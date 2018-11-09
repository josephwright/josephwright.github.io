---
title: Avoiding active characters
layout: post
permalink: /2009/07/04/avoiding-active-characters/
categories:
  - Packages
  - siunitx
---
A while ago, I had a bug report for [`siunitx`](https://ctan.org/pkg/siunitx), which gives an infinite loop if used with [`htlatex`](http://www.cse.ohio-state.edu/~gurari/TeX4ht/mn-commands.html).  It has taken me a while to work out where the problem was, but it comes down to the use of active characters. I've given it some thought, and now have a solution that will work in the development version of `siunitx`. I'm currently reluctant to modify the release version to alter this behaviour, because it is quite a big change. If this is an issue for lots of people, I'll revisit this, of course.

Hopefully, UTF-8 capable engines ([XeTeX](https://tug.org/xetex/) and [LuaTeX](http://www.luatex.org)) will mean that the general use of active characters can be avoided. There are a lot of pitfalls, and in general it seems to be much better to steer well clear unless absolutely necessary.
