---
id: 427
title: EPS graphics with PDF(La)TeX
date: 2009-09-28T16:29:13+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=427
permalink: /2009/09/28/eps-graphics-with-pdflatex/
categories:
  - LaTeX3
tags:
  - EPS
  - MiKTeX
  - PDF
  - pdfTeX
  - TeX Live
---
One issue a lot of people find confusing with (La)TeX is the rules about which types of graphic files work with which engines. EPS files are fine when going <em>via </em>the DVI route, but do not work with direct PDF creation. The solution is to turn the EPS files in PDFs, and the problem goes away. However, there is then the question of how to do the conversion.

For most documents, having to convert every file by hand is not a sensible choice. The next nearest thing is the <a title="Convert EPS to &#039;encapsulated&#039; PDF using GhostScript" href="http://ctan.org/pkg/epstopdf">epstopdf</a> package, which will do the same thing but from within a LaTeX run. However, it needs <code>\write18</code> enabled, and this is not always desirable. More importantly, a lot of people who struggle with the graphics problem do not know how to turn on <code>\write18 </code>anyway. A good way around has been added to the latest version of <a title="TeX Live" href="http://www.tug.org/texlive">TeX Live</a>, which is currently in the final testing stages. TeX Live 2009 has some restricted <code>\write18</code> functions enabled as standard, and also has a version of epstopdf “built in”. The result is that EPS files are automatically converted to PDF files, in a transparent manner. Of course, this only happens if the PDF does not also exist! At the moment, this feature is not in MiKTeX 2.8, so it is one reason to favour TeX Live 2009 even on Windows.

There are places where epstopdf will not help: for example, when using <a title="Replace strings in encapsulated PostScript figures" href="http://ctan.org/pkg/psfrag">psfrag</a> or <a title="PostScript macros for TeX" href="http://ctan.org/pkg/pstricks">pstricks</a>. There, the best solution will either be <a title="Wrapper for pst-pdf (with some psfrag features)" href="http://ctan.org/pkg/auto-pst-pdf">auto-pst-pdf </a>or <a title="Support for psfrag within pdfLaTeX" href="http://ctan.org/pkg/pstool">pstool</a>. Both are written by Will Robertson, and both need <code>\write18</code> enabled to work. pstool is more efficient (it only re-creates graphics as needed), but for some cases on auto-pst-pdt will work. Will has documented both packages very well, so the best way to learn about them is to have a read of the documentation.
