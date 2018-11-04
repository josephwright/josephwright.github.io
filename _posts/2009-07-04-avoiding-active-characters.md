---
id: 340
title: Avoiding active characters
date: 2009-07-04T08:34:16+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=340
permalink: /2009/07/04/avoiding-active-characters/
categories:
  - Packages
  - siunitx
---
A while ago, I had a bug report for <a title="A comprehensive (SI) units package" href="http://www.ctan.org/pkg/siunitx">siunitx</a>, which gives an infinite loop if used with <a href="http://www.cse.ohio-state.edu/~gurari/TeX4ht/mn-commands.html">htlatex</a>.  It has taken me a while to work out where the problem was, but it comes down to the use of active characters. I've given it some thought, and now have a solution that will work in the <a href="http://developer.berlios.de/projects/siunitx/">development version</a> of siunitx. I'm currently reluctant to modify the release version to alter this behaviour, because it is quite a big change. If this is an issue for lots of people, I'll revisit this, of course.

Hopefully, UTF-8 capable engines (<a title="XeTeX" href="http://www.tug.org/xetex/">XeTeX</a> and <a title="LuaTeX homepage" href="http://www.luatex.org">LuaTeX</a>) will mean that the general use of active characters can be avoided. There are a lot of pitfalls, and in general it seems to be much better to steer well clear unless absolutely necessary.