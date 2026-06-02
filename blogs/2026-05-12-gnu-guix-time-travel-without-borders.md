---
title: 'GNU Guix: Time travel without borders'
url: https://guix.gnu.org/blog/2026/time-travel-without-borders//
date: '2026-05-12'
author: ''
feed_url: https://planet.gnu.org/rss20.xml
---
When offered the option to run other peopleâ€™s code, a prime
consideration is often ease of deployment.  While much progress has been
made in support of rapid deployment, the security implications of those
quick deployments is often overlooked.  In this post, we look at a new
feature of guix time-machine and guix pull in support of one-line
deployment commands : the ability to download channel files, but without
compromising on security. Sharing code The normal workflow to share software and make it easily deployable with
Guix goes like this: someone puts their packager hat on and writes a
package definition, adds it to Guix proper or to a separate channel ,
at which point anyone can fetch the relevant channel(s) and deploy the
software. As an example, letâ€™s assume you want to run yt-dlp as packaged in
the latest Guix revision without upgrading your system or going through
an explicit installation step.  The simplest way to do that is with this
command: guix time-machine -q -- shell yt-dlp -- yt-dlp â€¦ If youâ€™re familiar with Nix, this is equivalentâ€”with some important
differences weâ€™ll discuss belowâ€”to this command: nix shell nixpkgs#yt-dlp --command yt-dlp â€¦ In both cases, weâ€™re fetching the latest revision of the package
collection (the master branch for Guix, the nixpkgs-unstable branch
of Nixpkgs for Nix) and running yt-dlp from there.  ( nix run goes one step further by removing the need to specify the command name.) Now, that was an easy example because yt-dlp comes from Guix itself.
What if youâ€™d like to deploy an application thatâ€™s in another channel
such as Guix-Science ?
Well, you would first need to come up with a channels.scm file for
Guix-Science and then you
can pass it to guix pull or guix time-machine : $EDITOR channels.scm
# Make sure that includes Guix-Science.
guix time-machine -C channels.scm -- shell â€¦ If youâ€™re lucky, perhaps you can download a channel file.  For example, Cuirass produces them for all
successfully-evaluated commits, so you can fetch one for
Guix-Science and go from there: wget -O channels.scm \
  https://guix.bordeaux.inria.fr/eval/latest/channels.scm?spec=guix-science
guix time-machine -C channels.scm -- shell â€¦ You can even do it in a single command using Bash process
substitution ! guix time-machine \
  -C <(wget -O https://guix.bordeaux.inria.fr/eval/latest/channels.scm?spec=guix-science) \
  -- shell â€¦ Is it a good idea though? The threat If you look more closely, the nix shell command and the last two guix time-machine commands have a bit of a curl | sh flavor to it:
downloading arbitrary code and running it without further ado.  All nix shell does is authenticate github.com , through HTTPS, and likewise
for wget â€”that youâ€™re downloading from the genuine github.com doesnâ€™t
tell you anything about the trustworthiness of the code youâ€™re running. In the case of Guix, the channels.scm youâ€™re downloading could very
well read this: (system* "rm" "-rf" "/")  ;uh-oh! Here system* , as you might have guessed, invokes a
command .
Because yes, channel files can contain arbitrary Scheme code!  (Itâ€™s
worth noting that this particular problem is one Nix doesnâ€™t have: Nix
being a domain-specific language (DSL) already limits what Nix code can
do, especially with so-called â€œpureâ€� evaluation.) Or it could read something like this: (list (channel
        (name 'guix)
        ;; This is Malloryâ€™s malicious Guix, now youâ€™re PWND!
        (url "https://example.org/EVIL/guix.git")
        (branch "master")
        (introduction
         (make-channel-introduction
          "badc0ffeed807b096b48283debdcddccfea34bad"
          (openpgp-fingerprint
           "DEAD CABB A99E F6A8 0D1D  E643 A2A0 6DF2 A33A BADD"))))) In this case, the channel file looks good, but the channel youâ€™ll
fetchâ€”probably not so much. So no: downloading a channel file and using it without checking it is
not reasonable. The cake Can we have our cake and eat it too?  Can we casually download someone
elseâ€™s channel file without putting our system at risk? Changes that have just landed in guix pull and guix time-machine aim
to address these seemingly contradictory needs.  The two commands are
now equipped to download by themselves: just pass them a URL with the -C (or --channels ) option. guix time-machine \
  -C https://ci.guix.gnu.org/eval/latest/channels.scm?spec=master \
  -- â€¦ Crucially, this command is not equivalent to the naÃ¯ve -C <(wget -O â€¦) trick we saw above. First, channel code is now evaluated in a
â€œsandboxâ€� :
it can only access a predefined set of bindings, cannot import
additional modules, and it must run in a limited amount of time and with
a limited amount of memory allocated.  This still provides access to
many general-purpose facilities but blocks anything that could be used
to alter the system state, exfiltrate data, or cause a denial of
service. With this in place, evaluating a channel file can be considered safe.
Now, one problem remains: the file might list channels that I as a user
do not trust.  And here we see a tension between fetching channel files from out there and keeping oneâ€™s system safe.  To address that, we
define a new rule: only trusted channels may be deployed; if a channel
file lists untrusted channels, guix pull and guix time-machine error
out.  Trusted channels are defined as follows: they are those listed in ~/.config/guix/trusted-channels.scm , if
it existsâ€”this file lists channels just like a regular channel file; or, they are the channels currently in use, as returned by guix describe . This brings us to the interesting question of channel identity .  This
channel I call guix-science in my trusted-channels.scm , someone else
might as well call it Guix-Science or science ; how can I tell if
weâ€™re dealing with the channel that I call guix-science and that I
trust? The key insight is that the name itself doesnâ€™t matter; the element that does matter is the â€œintroductionâ€� of the channelâ€”the piece of
information that tells how to authenticate updates of that
channel .  If you
forgot that episode, the introduction the thing with hexadecimal strings
that appears in a channel specification: (channel
  (name 'guix-past)
  (url "https://codeberg.org/guix-science/guix-past")
  (introduction   ;this hex soup ğŸ‘‡ is the channelâ€™s identity
   (make-channel-introduction
    "0c119db2ea86a389769f4d2b9c6f5c41c027e336"
    (openpgp-fingerprint
     "3CE4 6455 8A84 FDC6 9DB4  0CFB 090B 1199 3D9A EBB5")))) Two channels with the same introduction are one and the same.  Thus, if
my trusted-channels.scm contains a channel with the above
introduction, pull and time-machine will happily pull from it. The corollary is that a channel that cannot be authenticatedâ€”i.e., that
lacks the introduction fieldâ€”cannot be considered a trusted channel. Overall, this â€œtrusted channelâ€� rule trades flexibility for safety.
Itâ€™s a tradeoff but one that looks like a better default than anything
that effectively amounts to arbitrary code execution Ã  la curl | sh . The party â€œWhy would I want to download channel files?â€�, you may ask?  Hereâ€™s a
list of typical use cases we have in mind. The first one is downloading a channel file from a continuous
integration systemâ€”to deploy from a known-good state, to test a new
package version or a new feature, to reproduce a bug, etc. Cuirass serves channel files for
every channel set it evaluates.  So for example, you can pull the latest
Guix channel that was successfully evaluated like this: guix pull -C https://ci.guix.gnu.org/eval/latest/channels.scm?spec=master Likewise, this is how youâ€™d travel to the latest Guix-Science channel
and dependent
channels to execute RStudio: guix time-machine \
  -C https://guix.bordeaux.inria.fr/eval/latest/channels.scm?spec=guix-science
  -- shell rstudio -- rstudio A second, similar use case is one-line commands for demos : if youâ€™re
developing an application, you can package it, publish a channel file,
and share a time-machine command to spawn it.  With pinned
channels ,
you can ensure users run it from a known-good state. A third use case that is emerging is channel releases .  Teams
maintaining third-party channels might want to tag releases of their
channel as a channel files where each channel is pinned.  This is what the Guix-Science project recently decided to
do . In the same vein, a fourth use case is the publication of a tested
channel file that a whole team, or a whole fleet of computers, would
upgrade from.  Imagine a group of people responsible for testing who
would periodically publish a new channel file pinned to known-good
commits that all the team members or an entire fleet could safely pull
fromâ€”it could even be used for unattended
upgrades ! The fifth use case is reproducible
research .
A computational workflow can be captured by two files: channels.scm and manifest.scm .  In some cases, we
might as well download the channel file. Dissonance? But waitâ€¦ the astute reader might have felt some dissonance: downloading a channel file to set up a supposedly reproducible
workflow?  That canâ€™t be right: the channel file could change over time,
or it could vanish from its original URL.  Thatâ€™s not reproducibility,
is it? As Simon Tournier was prompt to suggest ,
the solution is to support SWHIDs (Software Hash
Identifiers) in addition to URLs.  A SWHID is essentially a standardized
content hash that uniquely identifies â€œcontentâ€�â€”raw data or structured
data such as directories and version-control revisions.  If you followed
along, you might remember that Guix is connected to the Software
Heritage
archive .
Software packaged in Guix is in the
archive and so all we had to do
is connect the dots. Consider this command: guix time-machine \
  -C swh:1:cnt:003e1e0c1b9b358082201332c926ae54e9549002  \
  -- â€¦ It downloads the channel file identified by the given
SWHID and then proceeds. The SWHID serves as an unambiguous and unique content address to refer
to a specific channel set.  It can be computed using guix hash ,
but of course, the channel file must first be present in the Software
Heritage archive.  Thus, if the file is part of a version-control
repository, you can first request archiving of that
repository .  In a research
paper, one may include a single command to re-run computations the paper
builds upon. Pleasurable This new addition felt pleasurable for several reasons.  First because
it addresses use cases that people had been talking for a while, and
itâ€™s always nice to fill gaps.  It also felt good because several design
choices complement each other so that everything here falls into place:
channel specifications, Guileâ€™s â€œsandboxingâ€�, channel authentication,
and Software Heritage integration. The whole endeavorâ€”allowing for quick deployment without compromising on
securityâ€”might sound quixotic or, some might say, anachronistic, at a
time when the pip s , the npm s ,
the snap s and many more are all about deploying software of unknown origin like
thereâ€™s no tomorrow.  In Guix we do believe that transparency,
provenance tracking, and verifiability matter for the software we run;
efforts like this one are guided by these principles. The feature landed just a
few days ago.  Give it a try and letâ€™s hope you find it pleasant as
well! Acknowledgments I am grateful to Caleb â€œReepcaâ€� Ristvedt for their thorough code review
and insightful suggestions, and to Simon Tournier for commenting on the
general approach and suggesting improvements.  Many thanks to Rutherther
and to Cayetano Santos for reviewing an earlier draft of this post.
