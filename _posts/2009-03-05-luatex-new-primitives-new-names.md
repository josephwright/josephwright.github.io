---
id: 213
title: 'LuaTeX: new primitives, new names'
date: 2009-03-05T19:13:03+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=213
permalink: /2009/03/05/luatex-new-primitives-new-names/
categories:
  - General
tags:
  - LuaTeX
  - XeTeX
---
There has been quite a bit of dicussion recently on the <a title="LuaTeX Mailing List" href="http://tug.org/pipermail/luatex/">LuaTeX mailing list</a> about primitive names.  The basic set of primitive names provided by TeX has already been extended by e-TeX, <a title="pdfTeX Homepage" href="http://www.tug.org/applications/pdftex/">pdfTeX</a> and <a title="XeTeX Homepage" href="http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=xetex">XeTeX</a>. While e-TeX primitives have names which express only the function (such as <code>\detokenize</code>), both pdfTeX and XeTeX have tended to add the engine name to all new primitives. So for example pdfTeX provides the <code>\pdfprimitive</code> function, which always carries out the orginial function of a name, even if it has later been redefined:
<pre>\let\everypar\undefined
% \everypar{Some stuff} % Gives an error
\pdfprimitive\everypar{Some stuff}</pre>
will, for example, add material to <code>\everypar</code> despite the redefinition.

In <a title="LuaTeX Homepage" href="http://www.luatex.org/">LuaTeX</a>, the idea of adding an engine-specific prefix has been abandoned. The example above shows one reason why: <code>\pdfprimitive</code> makes more sense with the name <code>\primitive</code> (which is what LuaTeX calls it). The problem with this is that name clashes are marginally more likely without a prefix (for example, <code>\expanded</code> is used in <a title="ConTeXt Homepage" href="http://wiki.contextgarden.net/Main_Page">ConTeXt</a> as a macro, but this is planned as a primitive for pdfTeX 1.50).

On the other hand, LuaTeX is a fundamental break with previous engines, as the internal changes mean that it may give different line breaks and so on to earlier systems. Thus the argument for new, logical, primitive names is that moving to LuaTeX is not the same as moving from TeX to pdfTeX or pdfTeX to XeTeX. There will be changes, and the user (or package developer) will need to think about them before diving in.

Overall, I think the LuaTeX idea is the best in the long term. Primitives which have well specified names help everyone, and some times change is necessary. I'll be interest to see if the <code>\directlua</code> primitive for actually using Lua ends up with a shorter name (just <code>\lua</code>, anyone?).
