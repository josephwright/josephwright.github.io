---
id: 371
title: Testing MiKTeX 2.8 and TeX Live 2009
date: 2009-08-02T11:52:05+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=371
permalink: /2009/08/02/testing-miktex-2-8-and-tex-live-2009/
categories:
  - TeXworks
tags:
  - MiKTeX
  - TeX Live
  - XeTeX
---
Both <a title="MiKTeX Project Page" href="http://www.miktex.org/">MiKTeX</a> and <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> have new versions in the offing.  I've been testing out both MiKTeX 2.8 and TeX Live 2009, to keep up to date with what is happening. In the past, I've tended to stick with MiKTeX as it is designed for Windows, and so can make some platform-specific decisions and be more focussed. However, the TeX Live team have done a lot of work to make TeX Live usable across platforms, and there are advantages to that approach.

Looking through the feature lists, a lot of the new features are common to the two systems, for example:
<ul>
	<li><a title="TeXworks - lowering the entry barrier to the TeX world" href="http://www.texworks.org">TeXworks</a> installed as a distribution-maintained editor.</li>
	<li><a title="XeTeX on the Web" href="http://www.tug.org/xetex/">XeTeX</a> version 0.9995 (which includes the new primitives that the <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> team asked for).</li>
	<li>Some <code>\write18</code> functions enabled without turning on full <code>\write18</code> support: this is used to allow “safe” functions.</li>
</ul>
There are, of course, also differences. For example, only TeX Live includes <a title="Luatex home page" href="http://www.luatex.org">LuaTeX</a> at present. I also notice that MiKTeX 2.8 is adding the full path of files to the log, whereas in the past you got the relative path. I'm not so sure this is a good idea: it makes things rather wordy, and also the log will vary between systems: not so great. On the other hand, MiKTeX 2.8 does provide user-specific texmf directories. For multi-user systems, this is a real bonus: you can use the auto-install system without needing to be the Administrator.

As I said, I've tended to use MiKTeX to date as it's been the best “fit” on Windows. The latest version of TeX Live makes this a pretty tight call, I think. If you are happy installing a full TeX system (which I do), then there is very little in it. MiKTeX still has the edge for small installations, as the auto-install system really pays off there.