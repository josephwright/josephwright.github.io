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
Regular expressions are very popular as a quick and powerful way to carry out searches and replacements in text of all sorts. Traditionally, TeX handles tokens and not strings or characters. This means that doing regex searches using TeX82 is pretty much impossible. To solve this, recent versions of <a title="pdfTeX" href="http://www.pdftex.org">pdfTeX</a> adds the <code>\pdfmatch</code> primitive to allow real <em>string </em>matching inside TeX. The <a title="LuaTeX homepage" href="http://www.luatex.org">LuaTeX</a> team have decided not to take all of the existing “new” primitives forward from pdfTeX, and as I understand it  <code>\pdfmatch</code> will not be implemented in LuaTeX. However, Lua itself has regular expression matching, and so the functionality will still be around.

I've recently talked about <a href="http://www.texdev.net/2009/05/17/more-on-xetex-primitives/">adding new primitives to XeTeX</a>, and you'll see that <code>\pdfmatch</code> was not on the list for adding to <a title="XeTeX" href="http://www.tug.org/xetex/">XeTeX</a>. The reason is that a XeTeX implementation would have to be slightly different from pdfTeX, as it is natively UTF-8, but also would be different to LuaTeX, as it would still be a TeX primitive and not a Lua function. So here “the prize wasn't worth the winning”, in my opinion. As it is,  using <code>\pdfmatch</code> is not widespread, and the idea of having three different regex methods inside TeX didn't seem like a great idea!

Talking of regex implementations, I've been reading <a title="Programming in Lua" href="http://www.amazon.com/exec/obidos/ASIN/8590379825/lua-home-20"><em>Programming in Lua</em></a>, and also working with <a title="TeXworks: lowering the entry barrier to the TeX world" href="http://www.tug.org/texworks">TeXworks</a> to try to get syntax highlighting the way I like it. Both systems are slightly different, and it seems both are different from the <a title="Perl" href="http://www.perl.org">Perl</a> implementation. It seems that every time you want to use a regex system you have to read the manual to see which things are different from every other implementation!
