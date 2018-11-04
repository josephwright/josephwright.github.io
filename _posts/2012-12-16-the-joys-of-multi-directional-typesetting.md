---
id: 1574
title: The joys of multi-directional typesetting
date: 2012-12-16T16:28:56+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1574
permalink: /2012/12/16/the-joys-of-multi-directional-typesetting/
categories:
  - General
tags:
  - Aleph
  - bidi
  - Omega
  - right-to-left
  - TeX--XeT
---
<p>Anyone who subscribes to the <a href="http://tug.org/mailman/listinfo/xetex">XeTeX</a> or <a href="http://tug.org/mailman/listinfo/luatex">LuaTeX</a> mailing lists will have seen a lot of posts from me over the past couple of weeks, pursuing various aspects of multi-directional typesetting. That might prompt some questions, not least what has raised this interest!</p>

<p>I got a bug report for <a href="http://ctan.org/pkg/siunitx"><code>siunitx</code></a> a little while ago about interaction with the <a href="http://ctan.org/pkg/bidi"><code>bidi</code></a> package. That pushed me to look at something I've been wondering about for a while: what we need to do in the LaTeX3 codebase to allow for multiple directions (particularly right-to-left, which as <code>bidi</code> <em>shows</em> should be usable directly in LaTeX). It's turned out that good documentation on the various primitives available is not so easy to come by, and that there is a lot to get your head around. Luckily, I've had some very useful feedback from a range of people, including John Plaice (one of the authors of <a href="http://en.wikipedia.org/wiki/Omega_%28TeX%29">Omega</a>). It also turns out that not everything is quite settled in engine support for multiple directions, so asking questions is pretty important.</p>
