---
id: 309
title: LaTeX3 snapshot release
date: 2009-06-09T17:02:53+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=309
permalink: /2009/06/09/latex3-snapshot-release/
categories:
  - LaTeX3
---
The <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3 Project</a> (of which I'm a member) have made a snapshot release of the current <a title="LaTeX3 development code" href="http://www.latex-project.org/code.html">LaTeX3 code</a> to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a> today. This is in two parts:

<ul>
    <li><a title="The expl3 bundle: low-level LaTeX3 coding" href="http://www.ctan.org/pkg/expl3">expl3</a>, the base layer for LaTeX3, which provides a consistent programming interface for LaTeX3 on top of TeX (or rather, on top of <a title="pdfTeX" href="http://www.pdftex.org">pdfTeX</a>, <a title="The XeTeX typesetting system" href="http://www.tug.org/xetex/">XeTeX</a> or <a title="LuaTeX Homepage" href="http://www.luatex.org">LuaTeX</a>).</li>
    <li><a title="The xpackages bundle: high-Level LaTeX3 concepts" href="http://www.ctan.org/pkg/l3packages">xpackages</a>, higher level interface ideas for LaTeX3.</li>
</ul>

expl3 is now reasonably stable: the code has been carefully reviewed and the Team are happy that what is there works well. There are gaps, and some of these are definitely on the “to do” list. On the other hand, the xpackages bundle is not so close to being finished. At the moment, it includes only the parts of the experimental code that look the closest to reaching some kind of conclusion. However, it is also the part that is actively being reviewed at the moment. So I expect changes!

I'm hoping that as expl3 gets distributed around the TeX world it will be possible to consider using it for coding new packages. The ideas in expl3 make coding much easier, over all, even if initially there is a lot to learn. Of course, delivering more of LaTeX3 will help in getting people interested as well. That is something I'm definitely keen on.