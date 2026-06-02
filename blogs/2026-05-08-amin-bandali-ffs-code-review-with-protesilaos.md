---
title: 'Amin Bandali: FFS code review with Protesilaos'
url: https://kelar.org/~bandali/gnu/emacs/ffs-code-review-prot.html
date: '2026-05-08'
author: ''
feed_url: https://planet.gnu.org/rss20.xml
---
In the recent weeks I've been engaging Prot as an Emacs coach to help
with doing review passes over my upcoming ffs package as I work on
polishing and documenting it in preparation for offering it for
inclusion in GNU ELPA. Yesterday we had our second session focused on ffs , which I recorded
and share publicly with everyone with Prot's permission, so that
others can also benefit from Prot's insights and experience as we
discuss various aspects of Emacs package development with the concrete
example of ffs . Here is the video recording of our session: Sorry, this embedded video will not work,
because your web browser does not support HTML5 video. [ please watch the video in your favourite streaming media player ]â€‹ You can view or download the full-resolution video from the Internet
Archive. I addressed most of Prot's feedback about ffs from our first
session, and I'll be working on the changes we discussed in this
session in the next days. In the last third of the video we switched topics to discuss a few
Emacs-related tangents including adding a 'padding' effect for the
mode line and its constructs, and distilling and separating the
easily-reusable package-like parts of one's Emacs configuration from
the actual configuration of those parts (e.g. the distinction of prot-lisp and prot-emacs-modules in Prot's Emacs configuration ). For mode line padding, here is the snippet I'm using with Prot's doric-themes : (doric-themes-with-colors
  (custom-set-faces
   `(mode-line
     ((t :box (:line-width 6 :color ,bg-shadow-intense))))
   `(mode-line-inactive
     ((t :box (:line-width 6 :color ,bg-shadow-subtle))))
   `(mode-line-highlight
     ((t :box (:color ,bg-shadow-intense)))))) Take care, and so long for now.
