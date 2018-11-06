---
id: 85
title: Universal UTF-8
date: 2009-01-06T13:13:45+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=85
permalink: /2009/01/06/universal-utf-8/
categories:
  - General
---
The existence of editors such as <a title="TeXworks homepage" href="http://www.texworks.org">TeXworks</a> make it very easy to work with UTF-8 source documents.  However, there are still a number of issues to thing about before deciding to use UTF-8 for all of your work.

First, there is the issue of other users.  If you are writing things that will not need to be edited by others, then the choice is down to you.  The moment you have collaborators, you need to ensure that they are also okay with UTF-8. They might be using an editor where this is not going to work (<a href="http://www.winedt.com">WinEdt</a>, for example). If you are preparing stuff for a publisher, you have to be even more careful, as they may have quite a “traditional” TeX system. I know that the <a href="http://pubs.acs.org">American Chemical Society</a> don't even have the e-TeX extensions, for example.

Then there are more technical issues.  If you are a LaTeX user, you might well also use BibTeX.  BibTeX is old, and as yet there is no real UTF-8 aware replacement.  So at least in a database of references you may have to stick with escape sequences or some other encoding.

There are also choices to make about the engine you use. XeTeX is the obvious choice for  UTF-8 documents, but that means missing out on the pdfTeX extensions to TeX, for example micro-typography. LuaTeX might help here, but if you are a <a href="http://www.miktex.org">MiKTeX</a> user this is still some way off being available.

All in all, UTF-8 input is not quite the universal standard for TeX, just yet. New editors and engines mean that things are almost there, but a few awkward issues remain.
