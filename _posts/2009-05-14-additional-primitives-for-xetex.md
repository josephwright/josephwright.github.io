---
id: 290
title: Additional primitives for XeTeX
date: 2009-05-14T19:34:04+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=290
permalink: /2009/05/14/additional-primitives-for-xetex/
categories:
  - General
tags:
  - pdfTeX
  - XeTeX
---
[XeTeX](https://tug.org/xetex/) has, over the past few years, made using TeX with multiple fonts and UTF-8 input easy.  The work-flow using XeTeX is very much more accessible than the routes needed using [pdfTeX](http://www.pdftex.org) or TeX82. So I'm sure that many people, like me, use XeTeX whenever they want to use arbitrary fonts or to write anything which doesn't use western European characters.

XeTeX is based on [ε-TeX](https://tug.org/texmf-dist/doc/etex/base/etex_ref.html), which means it has a number of primitives which were not present in TeX82, but are present in ε-TeX itself or in pdfTeX (which also includes the ε-TeX primitives). However, ε-TeX was finalised over ten years ago, and since then the pdfTeX team have added a number of new primitives, many related directly to PDF output. At the same time, XeTeX includes its own new or extended primitive functions, in this case focussed on UTF input. For the most part this does not concern people as things work fine.

Recently, there has been some testing of the current [LaTeX3](https://www.latex-project.org/latex3.html) code with XeTeX (and older versions of pdfTeX, which don't have all of the newer primitives). LaTeX3 requires the  ε-TeX extensions, which are as I said available with any modern TeX engine. However, when it's available LaTeX3 also uses the `\pdstrcmp` primitive: this is only present in _newer_ versions of pdfTeX. For those people not familiar with `\pdstrcmp`, it allows you to do _string_ comparisons of text (not token comparisons), and in an expandable manner.  This is very useful, and much better than doing things without it; with no `\pdfstrcmp`, comparisons are not expandable. It became clear that there is a danger of some things working when using newer versions of pdfTeX, but failing with older ones or with XeTeX. Older versions of pdfTeX is one thing (the advice can simply be “sorry, you'll have to update your pdfTeX”), but failing with XeTeX is simply no acceptable. After a bit of discussion, the best solution seemed to be to talk to Jonathan Kew about getting a very small number of “new” pdfTeX primitives into XeTeX.

At the moment, things are still under discussion, but the list of additional primitives is going to be small (somewhere between 2 and 5 seems likely). I think it's giving nothing away to say that `\pdfstrcmp` is one that really is needed (although the name might be an issue!). Another likely candidate is `\ifincsname`, which looks handy and also not too complex to implement. There are a few other suggestions, but I'm not sure just yet what will be really _needed_, as opposed to nice to have. What is clear is that this is a one-off request. Once these small gaps are filled, LaTeX3 will not be using other primitives for general functions. I'm not sure how long it will take to finalise things, both for the team to agree on what is needed and for Jonathan Kew to do the hard work, but I'd imagine weeks not longer.
