---
id: 1586
title: Clipping support in XeTeX
date: 2013-02-04T09:04:09+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1586
permalink: /2013/02/04/clipping-support-in-xetex/
categories:
  - General
tags:
  - graphics
  - xdvipdfmx
  - XeTeX
---
Clipping boxes is something that TeX does not do: it simply places them on the page. That means that clipping graphics (a pretty common requirement) is actually done by the driver rather than by TeX. The LaTeX `graphics` package and the driver support that come with it cover quite a lot of cases, and over the years support for a number of other drivers have been written based on the same ideas. However, things are still not 100% identical over all back-ends. A particular gap at the moment is that that XeTeX support code does not offer clipping, because the XeTeX engine does not do this (pdfTeX and LuaTeX both do). Users of [`pgf`](https://ctan.org/pkg/pgf) might have noticed that it manages to do clipping perfectly happily with XeTeX (or rather they might have wondered why `graphics` doesn't when `pgf` does). Martin Scharrer and I looked at this a while ago for his [`adjustbox`](https://ctan.org/pkg/adjustbox) package, and worked out what is actually needed: some PostScript specials in a `xdvipdfmx` wrapper. The same basic idea is now being integrated into `xetex.def`, the driver support code used by `graphics`. This will go to CTAN soon, but some testing would be good. The [updated file is available now](https://texdev.net//wp-content/uploads/2013/02/xetex.def), so I'd encourage intrepid readers to download and test it!
