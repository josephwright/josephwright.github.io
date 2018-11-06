---
title: Standard font loading in LaTeX2e with XeTeX and LuaTeX
layout: post
permalink: /2016/12/20/standard-font-loading-in-latex2e-with-xetex-and-luatex/
categories:
  - General
tags:
  - fonts
  - LaTeX2e
  - LuaTeX
  - Unicode
  - XeTeX
---
The [LaTeX Project](https://latex-project.org/) have been making efforts over the past few years to update support in the [LaTeX2e kernel](https://ctan.org/pkg/latex) for XeTeX and LuaTeX. Supporting these Unicode-enabled engines provide new features (and challenges) compared to the 'classical' 8-bit TeX engines (probably pdfTeX for most users). Over recent releases, the team have made the core of LaTeX 'engine-aware' and pulled a reasonable amount of [basic Unicode data](https://ctan.org/pkg/unicode-data) directly into the kernel. The next area we are addressing is font loading, or rather the question of what the out-of-the-box (text) font should be.

To date, the LaTeX kernel has loaded Knuth's Computer Modern font in his original 'OT1' encoding for all engines. Whilst there are good reasons to load at least the T1-encoded version rather than the OT1 version, using an 8-bit engine using the OT1 version can be justified: it's a question of stability, and nothing is actually out-and-out wrong.

Things are different with the Unicode engines: some of the basic assumptions change. In particular, there are some characters in the upper-half of the 8-bit range for T1 that are not in the same place in Unicode. That means that hyphenation will be wrong for words using some characters _unless_ you load a Unicode font. At the same time, both LuaTeX and XeTeX have changed a lot over recent years: stability in the pdfTeX sense isn't there. Finally, almost all 'real' documents using Unicode engines will be loading the excellent [`fontspec`](https://ctan.org/pkg/fontspec) package to allow system font access. Under these circumstances, it's appropriate to look again at the standard font loading.

After careful consideration, the team have therefore decided that as of the next (2017) LaTeX2e release, the standard text font loaded when XeTeX and LuaTeX are in use will be [Latin Modern](http://www.gust.org.pl/projects/e-foundry/latin-modern) as a Unicode-encoded OpenType font. (This is the font chosen by `fontspec` so for almost all users there will no change in output.) No changes are being made to the macro interfaces for fonts, so users wanting anything other than Latin Modern will continue to be best served by loading `fontspec`. (Some adjustments are being made to the package to be ready for this.)

It's important to add that no change is being made in math mode: the Unicode maths font situation is not anything like as clear as the text mode case.

There are still some details being finalised, but the general approach is clear and should make life easier for end users.
