---
title: LuaTeX reachs 0.40
layout: post
permalink: /2009/04/23/luatex-reachs-040/
categories:
  - General
tags:
  - LuaTeX
---
A recent announcement on the [LuaTeX mailing list](https://tug.org/pipermail/luatex/) that [LuaTeX](http://www.luatex.org) has reached v0.40 has been expected for a while. One of the most notable, and widely discussed, changes is in the way new primitives are made available. As of 0.40, 'out of the box' LuaTeX only provides one new primitive, `\directlua`. To get any primitives beyond those from TeX82, you then have to call Lua and get it to turn them on. The reason for this rather radical change is that it avoids any name clashes between new primitives and existing packages. So LuaTeX should, in principle, be able to replace pdfTeX as the engine of choice for most people. Of course, that is still some way off: LuaTeX is scheduled to reach version 1.0 in 2012.
