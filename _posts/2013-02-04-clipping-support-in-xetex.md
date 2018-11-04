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
<p>Clipping boxes is something that TeX does not do: it simply places them on the page. That means that clipping graphics (a pretty common requirement) is actually done by the driver rather than by TeX. The LaTeX <code>graphics</code> package and the driver support that come with it cover quite a lot of cases, and over the years support for a number of other drivers have been written based on the same ideas. However, things are still not 100% identical over all back-ends. A particular gap at the moment is that that XeTeX support code does not offer clipping, because the XeTeX engine does not do this (pdfTeX and LuaTeX both do). Users of <a href="http://ctan.org/pkg/pgf"><code>pgf</code></a> might have noticed that it manages to do clipping perfectly happily with XeTeX (or rather they might have wondered why <code>graphics</code> doesn't when <code>pgf</code> does). Martin Scharrer and I looked at this a while ago for his <a href="http://ctan.org/pkg/adjustbox"><code>adjustbox</code></a> package, and worked out what is actually needed: some PostScript specials in a <code>xdvipdfmx</code> wrapper. The same basic idea is now being integrated into <code>xetex.def</code>, the driver support code used by <code>graphics</code>. This will go to CTAN soon, but some testing would be good. The <a href="https://texdev.net//wp-content/uploads/2013/02/xetex.def">updated file is available now</a>, so I'd encourage intrepid readers to download and test it!</p>
