---
id: 296
title: More on XeTeX primitives
date: 2009-05-17T14:40:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=296
permalink: /2009/05/17/more-on-xetex-primitives/
categories:
  - General
tags:
  - pdfTeX
  - XeTeX
---
There has been a bit more work on the idea of adding primitives to <a title="The XeTeX typesetting system" href="http://www.tug.org/xetex/">XeTeX</a> to match those available in <a title="pdfTeX" href="http://www.pdftex.org">pdfTeX</a>.The list of pdfTeX primitives which look interesting has grown slightly, and now reads:
<ul>
	<li><code>\ifincsname</code></li>
	<li><code>\ifpdfprimitive</code></li>
	<li><code>\pdfprimitive</code></li>
	<li><code>\pdfshellescape</code></li>
	<li><code>\pdfstrcmp</code></li>
</ul>
At the same time, it would be useful to include the “extended” version of <code>\vadjust</code> which pdfTeX makes available. This is something that has been <a title="[XeTeX] wanted: \vajdust pre" href="http://www.tug.org/pipermail/xetex/2008-August/010720.html">asked about before</a>, and as with the rest of the changes the main issue is not the idea of doing it but the time for actual implementation.

The real need to have <code>\pdfstrcmp</code> available for <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> work means that some effort has actually gone into this. I've got no experience with either Pascal or the <a title="The CWEB System of Structured Documentation " href="http://sunburn.stanford.edu/~knuth/cweb.html">WEB format</a>, but I've managed but dint of determination to get something passable to Jonathan Kew. There will need to be some adjustments, as XeTeX works with UTF-8 internally, which pdfTeX does not do. However, I'm hopeful that we will see new primitives in XeTeX soon.

Quite how the primitives will be named is still to be decided. The existing <code>\pdf...</code> naming does not really make sense with these non-PDF related functions. So they could end up as  <code>\XeTeX...</code> or may just be given generic names. I'm leaving that to Jonathan!
