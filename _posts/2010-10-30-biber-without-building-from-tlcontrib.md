---
id: 838
title: biber without building from TLContrib
date: 2010-10-30T07:40:27+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=838
permalink: /2010/10/30/biber-without-building-from-tlcontrib/
categories:
  - biblatex
  - Packages
tags:
  - biber
  - TeX Live
  - TLcontrib
---
I've <a href="http://www.texdev.net/index.php?s=biber">written in the past</a> about the <a title="Biber: BibTeX replacement for biblatex" href="http://biblatex-biber.sourceforge.net/">biber</a> program, a replacement for BibTeX when using the <a title="Bibliographies in LaTeX using BibTeX for sorting only" href="http://ctan.org/pkg/biblatex">biblatex</a> system for citations in LaTeX. The biggest stumbling block to using biber to date has been the need to build it from the source. On Windows, that also means getting a working <a title="Strawberry Perl for Windows" href="http://strawberryperl.com/">Perl</a> installation, which is a non-standard item on that operating system. However, there is now an alternative approach, at least for people using <a title="TeX Live" href="http://www.tug.org/texlive">TeX Live 2010</a>. The new <a title="TLContrib" href="http://tlcontrib.metatex.org/">TLContrib</a> system for additions to TeX Live now includes a <a href="http://tlcontrib.metatex.org/">biber package</a> for Windows, Mac OS X (64 bit) and Linux.

To get biber installed, you'll need to use the Command Prompt or Terminal. On Windows, you probably need to run the Command Prompt as the Administrator, while on the Mac or Linux you will  probably want to <code>sudo</code> the following. To get biber installed, all you need to type is

<pre>tlmgr --repository http://tlcontrib.metatex.org/2010 install biber</pre>

The system will then get on with installing biber, which you can then use as a replacement for BibTeX. I'd then add biber to my graphical editor's list of programs to make it easy to use: the detail of course depends on which editor you use.

What is particularly interesting here is that it has been possible to build a stand-alone biber. This should mean that at some stage both TeX Live and <a title="MiKTeX" href="http://www.miktex.org/">MiKTeX</a> can integer ate it directly. This will really make biber a viable choice for most people using biblatex: building from the source is not most people's idea of ‘easy to use’!