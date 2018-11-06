---
id: 1870
title: Managing biblatex backends
date: 2016-03-13T16:07:10+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1870
permalink: /2016/03/13/managing-biblatex-backends/
categories:
  - biblatex
  - Packages
---
For the past few years, [`biblatex`](https://ctan.org/pkg/biblatex) has been [looked after by a small team led by Philip Kime](http://www.texdev.net/2012/04/23/biblatex-a-team-to-continue-the-work/). When we first took this up we were mindful of the need to think carefully about back-ends: how reference data is extracted from a `.bib` file or similar sources.

There are currently two back-ends for `biblatex`: BibTeX and [Biber](http://biblatex-biber.sourceforge.net/). Biber is where the development is taking place and offers Unicode support, whilst BibTeX itself is frozen but also does a lot less 'stuff'. So there are several features in `biblatex` that are Biber-only. When the current team took over the maintained, there was consideration of dropping BibTeX entirely. Philip and I have discussed this quite a bit, as the original `biblatex` developer (Philippe Lehman) picked BibTeX as the original back-end from necessity. (Biber was developed after `biblatex`, and for extracting and sorting data there was only originally BibTeX.) We decided against it some time ago: what the BibTeX back-end offers is stability but also speed, precisely as it's more limited that Biber. At least for people like me, in the physical sciences and writing in western European scripts, the BibTeX back-end is perfectly usable.

The way we originally decided to allow continued Biber improvement but keep BibTeX use stable was to split the LaTeX code into two paths. That made sense with the proviso that new Biber features were essentially extensions to the code rather than any changes to existing ideas. However, over time that's not quite worked out, particularly recently with the new data model driven approach that Philip has developed for Biber. As I've [detailed elsewhere](http://www.texdev.net/2016/03/13/biblatex-a-new-syntax-for-declarenameformat/), that's led to a new (breaking) syntax for `\DeclareNameFormat`, as well as various other changes that could be covered in BibTeX but to-date haven't been. We've therefore decided we need to look again at this.

The current plan is for me to work on re-integrating the two back-end code paths, which I'm doing in a [fork of `biblatex`](https://github.com/plk/biblatex) as it's non-trivial and I don't want to mess the main development line up. I'll also look to extend the BibTeX back-end code as appropriate such that we get back to the differences being about the differing capabilities of the back-ends rather than anything in the LaTeX code. I need a little while to do that, probably a couple of months. However, if I get it right we should be in a much stronger position for the future.
