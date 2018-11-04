---
id: 325
title: Lowering the entry barrier
date: 2009-06-23T18:16:06+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=325
permalink: /2009/06/23/lowering-the-entry-barrier/
categories:
  - TeXworks
---
There has been a very active thread recently on the <a href="http://tug.org/pipermail/texworks/">TeXworks mailing list</a> concerning how the aim of “lowering the entry barrier to the TeX world” goes beyond the basics of the <a title="TeXworks: lowering the entry barrier to the TeX world" href="http://www.texworks.org/">TeXworks</a> interface. There are, as always, lots of ideas, with several very important points raised.

One big issue is the separation of TeX distributions, TeX engines and TeX editors. How do you explain to a new user that their editor is not their TeX system, and that their TeX system is independent of the engine they are using. This is all complicated, and it is not easy to put it into two or three sentences! All-in-one installers help to some extent, but that can lead to confusion later.

Another issue is which format to choose as the default. Currently, this is pdfTeX (plain TeX using the <a title="pdfTeX" href="http://www.pdftex.org">pdfTeX</a> engine). Is this a good choice for beginners? Probably not the best, but then almost every other choice has pluses and minuses. If you favour pdfTeX as the engine, using system fonts and Unicode input is more awkward. On the other hand, if <a title="XeTeX" href="http://www.tug.org/xetex/">XeTeX</a> is the default engine, then there are issues with micrography and interacting with other people. Then there is the <a title="The LaTeX Project" href="http://www.latex-project.org/">LaTeX</a> <em>versus</em> <a title="ConTeXt wiki main page" href="http://wiki.contextgarden.net/Main_Page">ConTeXt</a> choice, and again you can argue things both ways.

TeXworks is designed around PDF output. That is a good thing in the long term, but at the moment a lot of people still want to use the DVI route. Making that available from within TeXworks is hard to do in a cross-platform way (things that work on *nix fail on Windows).

There are other issues. For example, how much help should be built into TeXworks: again, the TeX format makes a difference here. Error-tracking is another awkward one: the differing formats again do different things.

There are a lot of difficult issues, and they are definitely worth thinking about. One day we'll have <a title="LuaTeX homepage" href="http://www.luatex.org">LuaTeX</a> finalised (and perhaps even <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a>), and some of these things will be sorted. But at the moment, there is lots to do.