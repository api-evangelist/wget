---
title: 'Amin Bandali: ffs 0.2.2 released'
url: https://kelar.org/~bandali/gnu/emacs/ffs-0.2.2.html
date: '2026-05-22'
author: ''
feed_url: https://planet.gnu.org/rss20.xml
---
ffs provides a minor mode for simple plain text presentations in
Emacs, where the slides are separated using the page-delimiter , by
default the form feed character ( ^L ). I wrote ffs in early 2022 for my LibrePlanet 2022 presentation the
Net beyond the Web , and earlier this year decided to polish it towards
being a proper package and submit it to GNU ELPA.  The manual still
needs some more work, but the overall package is in pretty good shape
so I submitted for inclusion in GNU ELPA. Package name (GNU ELPA): ffs Official manual: https://kelar.org/~bandali/gnu/emacs/ffs.html Change log: https://kelar.org/~bandali/gnu/emacs/ffs-changelog.html Git repository: https://git.kelar.org/~bandali/ffs Backronyms: fabulous foolproof slides - for freedom's sake -
ffs flips slides ffs and I owe a debt of gratitude to Protesilaos for rounds of
code review and feedback for improving and polishing the package in
preparation for submission to GNU ELPA.  You can watch videos of these
sessions posted earlier on my website: FFS code review with Protesilaos FFS code review and Emacs extensibility with Protesilaos Further, inspiration for parts of ffs 's implementation was
gratefully drawn from Protesilaos's Logos package for Emacs. Dedicated to the loving memory of Farangis Yousefinia . Below are the release notes. Version 0.2.2 on 2026-05-21 First release of ffs on GNU ELPA. The attempted build of ffs 0.2.1 within GNU ELPA build sandbox failed
with an Error: void-function (org-texinfo-kbd-macro) due to use of #+macro: kbd (eval (org-texinfo-kbd-macro $1)) in ffs.org for better
formatting of key sequences in the exported Texinfo copy.  This seems
to have happened for the specific case of generating a plain text
README using ox-ascii where ELPA didn't load ox-texinfo .  To try
and mitigate this, a README.md has been added for use as the package
README instead of ffs.org.  If not sufficient, a Texinfo copy of the
ffs manual will be shipped instead of the Org one in the next release. ffs 0.2.2 also includes small fixes and improvements throughout ffs.el from Stefan Monnier, and additional feedback to be addressed
in future releases. Version 0.2.1 on 2026-05-20 The attempted build of ffs 0.2.0 within GNU ELPA build sandbox failed
with a "Cannot include file" error on the "#+include: fdl.org" in the
manual.  So, as a workaround, we switch to using the official Texinfo
copy of the GNU FDL license rather than an Org copy. Version 0.2.0 on 2026-05-19 First release of ffs intended for GNU ELPA. After a few years of inactivity, in early 2026 I decided to dust off ffs.el , polish and document it, and offer for inclusion in GNU ELPA
as a proper package. Default value of ffs-default-face-height changed to nil To minimize unexpected and/or unnecessary changes out-of-the-box, the
default value of ffs-default-face-height has been changed to nil. ffs-edit-buffer-name demoted from user option to variable This is not an important user-facing setting, so to help avoid
overwhelming users with many options, this has been demoted from a
user option to a variable. Several new user options for customizing ffs 's behaviour As part of the effort to bring ffs more in line with the conventions
of other existing Emacs packages, the mechanisms for toggling various
parts of Emacs's interface to minimize visual clutter were changed
from being minor modes to being customizable user options.  These are
the replacement new user options, with a default value of nil: ffs-hide-cursor ffs-hide-mode-line ffs-hide-header-line Their value is buffer-local, and may be set globally using setq-default .  See the sample configuration in the manual for an
example of how to customize them. The new ffs-page-delimiter user option defines the page delimiter
inserted by ffs-edit-done when inserting a new slide.  Emacs's page-delimiter regexp should be able to match ffs-page-delimiter 's
value, so if you use a custom page-delimiter be sure to customize ffs-page-delimiter accordingly. The new ffs-echo-progress user option controls whether to display in
echo area the progress through the slides.  When non-nil, changing
slides will also display the progress through the slides in the echo
area.  The format of the displayed progress can be customized using
the new ffs-echo-progress-format user option. The new ffs-edit-display-buffer-alist user option may be used to
control the Window configuration for the ffs-edit buffer.  By
default, it will display the ffs-edit buffer in the same window. The new ffs-edit-done-hook user option may be used to define hooks
to be run at the end of ffs-edit-done after returning to the main ffs presentation buffer. Lastly, a new ffs-find-speaker-notes-function variable was added to
allow customizing the find function used for opening the speaker's
notes file, defaulting to find-file-other-frame . Version 0.1.0 on 2022-05-19 Initial publication of ffs.el as part of my personal configurations
for GNU Emacs. My first attempt at this concept was a now-archived ffsanim.el ,
a major mode implementation that used Emacs's animate library to
animate slide texts onto the screen.  Shortly after realizing the
shortcomings of that approach, I abandoned it in favour a minor mode
implementation and published version 0.1.0 of what is now ffs in
my personal configs repository . I used this implementation for presenting my LibrePlanet 2022 talk, The Net beyond the Web . I picked "ffs" as the package name, the acronym for form feed slides.
