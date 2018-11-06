---
title: EPS graphics with PDF(La)TeX
layout: post
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
One issue a lot of people find confusing with (La)TeX is the rules about which types of graphic files work with which engines. EPS files are fine when going _via_ the DVI route, but do not work with direct PDF creation. The solution is to turn the EPS files in PDFs, and the problem goes away. However, there is then the question of how to do the conversion.

For most documents, having to convert every file by hand is not a sensible choice. The next nearest thing is the [`epstopdf`](https://ctan.org/pkg/epstopdf) package, which will do the same thing but from within a LaTeX run. However, it needs `\write18` enabled, and this is not always desirable. More importantly, a lot of people who struggle with the graphics problem do not know how to turn on `\write18 `anyway. A good way around has been added to the latest version of [TeX Live](https://tug.org/texlive), which is currently in the final testing stages. TeX Live 2009 has some restricted `\write18` functions enabled as standard, and also has a version of epstopdf “built in”. The result is that EPS files are automatically converted to PDF files, in a transparent manner. Of course, this only happens if the PDF does not also exist! At the moment, this feature is not in MiKTeX 2.8, so it is one reason to favour TeX Live 2009 even on Windows.

There are places where epstopdf will not help: for example, when using [`psfrag`](https://ctan.org/pkg/psfrag) or [`pstricks`](https://ctan.org/pkg/pstricks). There, the best solution will either be [auto-pst-pdf ](https://ctan.org/pkg/auto-pst-pdf)or [`pstool`](https://ctan.org/pkg/pstool). Both are written by Will Robertson, and both need `\write18` enabled to work. pstool is more efficient (it only re-creates graphics as needed), but for some cases on auto-pst-pdt will work. Will has documented both packages very well, so the best way to learn about them is to have a read of the documentation.
