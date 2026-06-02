---
title: 'Amin Bandali: FFS code review and Emacs extensibility with Protesilaos'
url: https://kelar.org/~bandali/gnu/emacs/ffs-emacs-ext-prot.html
date: '2026-05-15'
author: ''
feed_url: https://planet.gnu.org/rss20.xml
---
In the recent weeks I've been engaging Prot as an Emacs coach to help
with doing review passes over my upcoming ffs package as I work on
polishing and documenting it in preparation for offering it for
inclusion in GNU ELPA. UPDATE 2026-05-15 08:50:10 -0400: Prot also published an article
about our session on his website: https://protesilaos.com/codelog/2026-05-15-emacs-amin-bandali-ffs-display-buffer-org-capture/ Today we had our third session where we started by reviewing and
talking about my recent changes to ffs , then ventured to other
Emacs-related topics with the overarching theme of the flexibility
and extensibility of GNU Emacs, including display-buffer-alist ,
keyboard macros, defining a custom ox-bhtml Org export backend
derived from Org's ox-html for ultimate flexibility when exporting
my site's pages from Org to HTML, Org capture, plain text files and
Emacs's diary and how it compares to org-agenda , and keeping a
journal with the help of Emacs. Here is the video recording of our session, which I share with Prot's
permission: Sorry, this embedded video will not work,
because your web browser does not support HTML5 video. [ please watch the video in your favourite streaming media player ]â€‹ You can view or download the full-resolution video from the Internet
Archive. Lastly, here is the snippet Prot shared for having Isearch treat space
as a wildcard, helpful for more easily matching multiple parts of a
line: (setq search-whitespace-regexp ".*?")
(setq isearch-lax-whitespace t)
(setq isearch-regexp-lax-whitespace nil) Take care, and so long for now.
