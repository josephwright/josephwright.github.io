---
title: XeTeX and LuaTeX: Directions
layout: post
permalink: /2009/01/11/xetex-and-luatex-directions/
categories:
  - General
tags:
  - LuaTeX
  - XeTeX
---
The XeTeX and LuaTeX engines both offer exciting ideas to the TeX user and the (La)TeX programmer. Using XeTeX, UTF-8 input is easy: no more awkward escape sequences. Font handling in XeTeX also makes it trivial to use any font installed on your system. On the other side of the equation, LuaTeX is going to bring a lot of useful programming tools to the TeX world. This should make some things a lot easier (handling floating point manipulation seems an obvious one), and make other things possible that are not currently.

The issue for me is the gaps between the two. XeTeX doesn't have things like microtypography (try loading the microtype package and doing a XeLaTeX run), and it's not clear to me how LuaTeX will work out with font handling. There's also the DVI _versus_ PDF issue: will we see a system where EPS, PNG, JPEG and PDF graphics can all be included without worrying about the engine in use? In many ways, I suppose these questions are more for the LuaTeX team to address: XeTeX has essentially delivered what it set out to do (a Unicode TeX which can use system fonts natively).
