---
id: 739
title: Pretesting TeX Live 2010
date: 2010-05-28T23:00:58+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=739
permalink: /2010/05/28/pretesting-tex-live-2010/
categories:
  - General
tags:
  - \write18
  - BibTeX
  - TeX Live
  - Unicode
---
The first [testing builds](http://www.tug.org/texlive/pretest) of TeX Live 2010 are now available, which you can also read about in the [TeXblog entry](http://texblog.net/latex-archive/news/tex-live-2010-test/). I downloaded it a few days ago, currently just to my Mac (Windows testing on my system at work starts next week). There are a few changes, some of which were planned for TeX Live 2009 and did not make it. The highlights for me

- Restricted `\write18` support is back. I've written about the [issues with this before](http://www.texdev.net/2009/10/14/no-restricted-write18-just-yet/), but as I understand it these are now solved. The idea of this support is that EPS graphics can be turned into PDF graphics automatically, meaning that pdfLaTeX is much easier to use for end users with mainly EPS graphics available.
- The default PDF output is level 1.5, which means that more compression of the output is available. The amount of compression depends on the type of output (files with lots of hyperlinks seem to show the most dramatic results). I've been using PDF 1.5 for a while with no issues, so I hope that this is applicable to most users.
- The is a Unicode version of BibTeX included: BibTeXU. I can't see any details of where this is coming from or the exact nature of the support: I hope to gain enlightenment at some stage. I'll certainly be testing it.

As I'm currently testing on my Mac, I've installed the 64-bit binaries (these still have to be installed in addition to MacTeX at the moment). I'm seeing slightly better performance with the 64 bit binaries than the 32 bit ones, but not by much. On Windows I'm currently limited to 32 bit, so there I'll have nothing to worry about!

So far, I've not had any major issues. TeX Live is very much evolution, not revolution, so that is not too much of a surprise. The team have done a good job, as usual, and I hope that others will brave the testing status of this release to help find any bugs before it's unleashed on the TeX world at large.
