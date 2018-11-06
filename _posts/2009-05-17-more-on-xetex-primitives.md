---
title: More on XeTeX primitives
layout: post
permalink: /2009/05/17/more-on-xetex-primitives/
categories:
  - General
tags:
  - pdfTeX
  - XeTeX
---
There has been a bit more work on the idea of adding primitives to [XeTeX](https://tug.org/xetex/) to match those available in [pdfTeX](http://www.pdftex.org).The list of pdfTeX primitives which look interesting has grown slightly, and now reads:

- `\ifincsname`
- `\ifpdfprimitive`
- `\pdfprimitive`
- `\pdfshellescape`
- `\pdfstrcmp`

At the same time, it would be useful to include the “extended” version of `\vadjust` which pdfTeX makes available. This is something that has been [asked about before](https://tug.org/pipermail/xetex/2008-August/010720.html), and as with the rest of the changes the main issue is not the idea of doing it but the time for actual implementation.

The real need to have `\pdfstrcmp` available for [LaTeX3](https://www.latex-project.org/latex3.html) work means that some effort has actually gone into this. I've got no experience with either Pascal or the [WEB format](http://sunburn.stanford.edu/~knuth/cweb.html), but I've managed but dint of determination to get something passable to Jonathan Kew. There will need to be some adjustments, as XeTeX works with UTF-8 internally, which pdfTeX does not do. However, I'm hopeful that we will see new primitives in XeTeX soon.

Quite how the primitives will be named is still to be decided. The existing `\pdf...` naming does not really make sense with these non-PDF related functions. So they could end up as  `\XeTeX...` or may just be given generic names. I'm leaving that to Jonathan!
