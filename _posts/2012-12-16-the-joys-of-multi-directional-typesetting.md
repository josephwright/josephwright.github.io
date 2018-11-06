---
title: The joys of multi-directional typesetting
layout: post
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
Anyone who subscribes to the [XeTeX](https://tug.org/mailman/listinfo/xetex) or [LuaTeX](https://tug.org/mailman/listinfo/luatex) mailing lists will have seen a lot of posts from me over the past couple of weeks, pursuing various aspects of multi-directional typesetting. That might prompt some questions, not least what has raised this interest!

I got a bug report for [`siunitx`](https://ctan.org/pkg/siunitx) a little while ago about interaction with the [`bidi`](https://ctan.org/pkg/bidi) package. That pushed me to look at something I've been wondering about for a while: what we need to do in the LaTeX3 codebase to allow for multiple directions (particularly right-to-left, which as `bidi` _shows_ should be usable directly in LaTeX). It's turned out that good documentation on the various primitives available is not so easy to come by, and that there is a lot to get your head around. Luckily, I've had some very useful feedback from a range of people, including John Plaice (one of the authors of [Omega](https://en.wikipedia.org/wiki/Omega_%28TeX%29)). It also turns out that not everything is quite settled in engine support for multiple directions, so asking questions is pretty important.
