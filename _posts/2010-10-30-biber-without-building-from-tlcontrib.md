---
title: Biber without building from TLContrib
layout: post
permalink: /2010/10/30/biber-without-building-from-tlcontrib/
categories:
  - biblatex
  - Packages
tags:
  - Biber
  - TeX Live
  - TLcontrib
---
I've written in the past about the [Biber](http://biblatex-biber.sourceforge.net/) program, a replacement for BibTeX when using the [`biblatex`](https://ctan.org/pkg/biblatex) system for citations in LaTeX. The biggest stumbling block to using Biber to date has been the need to build it from the source. On Windows, that also means getting a working [Perl](http://strawberryperl.com/) installation, which is a non-standard item on that operating system. However, there is now an alternative approach, at least for people using [TeX Live 2010](https://tug.org/texlive). The new [TLContrib](http://tlcontrib.metatex.org/) system for additions to TeX Live now includes a [Biber package](http://tlcontrib.metatex.org/) for Windows, Mac OS X (64 bit) and Linux.

To get Biber installed, you'll need to use the Command Prompt or Terminal. On Windows, you probably need to run the Command Prompt as the Administrator, while on the Mac or Linux you will  probably want to `sudo` the following. To get Biber installed, all you need to type is

```bash
tlmgr --repository http://tlcontrib.metatex.org/2010 install biber
```

The system will then get on with installing Biber, which you can then use as a replacement for BibTeX. I'd then add Biber to my graphical editor's list of programs to make it easy to use: the detail of course depends on which editor you use.

What is particularly interesting here is that it has been possible to build a stand-alone Biber. This should mean that at some stage both TeX Live and [MiKTeX](https://www.miktex.org/) can integer ate it directly. This will really make Biber a viable choice for most people using `biblatex`: building from the source is not most people's idea of 'easy to use'!
