---
id: 302
title: Regular expressions
date: 2009-05-30T16:27:38+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=302
permalink: /2009/05/30/regular-expressions/
categories:
  - General
tags:
  - LuaTeX
  - pdfTeX
  - regex
  - XeTeX
---
Regular expressions are very popular as a quick and powerful way to carry out searches and replacements in text of all sorts. Traditionally, TeX handles tokens and not strings or characters. This means that doing regex searches using TeX82 is pretty much impossible. To solve this, recent versions of [pdfTeX](http://www.pdftex.org) adds the `\pdfmatch` primitive to allow real _string_ matching inside TeX. The [LuaTeX](http://www.luatex.org) team have decided not to take all of the existing “new” primitives forward from pdfTeX, and as I understand it  `\pdfmatch` will not be implemented in LuaTeX. However, Lua itself has regular expression matching, and so the functionality will still be around.

I've recently talked about [adding new primitives to XeTeX](/2009/05/17/more-on-xetex-primitives/), and you'll see that `\pdfmatch` was not on the list for adding to [XeTeX](http://www.tug.org/xetex/). The reason is that a XeTeX implementation would have to be slightly different from pdfTeX, as it is natively UTF-8, but also would be different to LuaTeX, as it would still be a TeX primitive and not a Lua function. So here “the prize wasn't worth the winning”, in my opinion. As it is,  using `\pdfmatch` is not widespread, and the idea of having three different regex methods inside TeX didn't seem like a great idea!

Talking of regex implementations, I've been reading [_Programming in Lua_](http://www.amazon.com/exec/obidos/ASIN/8590379825/lua-home-20), and also working with [TeXworks](http://www.tug.org/texworks) to try to get syntax highlighting the way I like it. Both systems are slightly different, and it seems both are different from the [Perl](http://www.perl.org) implementation. It seems that every time you want to use a regex system you have to read the manual to see which things are different from every other implementation!
