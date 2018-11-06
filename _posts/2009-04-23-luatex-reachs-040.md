---
id: 276
title: LuaTeX reachs 0.40
date: 2009-04-23T07:12:21+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=276
permalink: /2009/04/23/luatex-reachs-040/
categories:
  - General
tags:
  - LuaTeX
---
A recent announcement on the <a href="http://tug.org/pipermail/luatex/">LuaTeX mailing list</a> that <a title="LuaTeX Homepage" href="http://www.luatex.org">LuaTeX</a> has reached v0.40 has been expected for a while. One of the most notable, and widely discussed, changes is in the way new primitives are made available. As of 0.40, “out of the box” LuaTeX only provides one new primitive, <code>\directlua</code>. To get any primitives beyond those from TeX82, you then have to call Lua and get it to turn them on. The reason for this rather radical change is that it avoids any name clashes between new primitives and existing packages. So LuaTeX should, in principle, be able to replace pdfTeX as the engine of choice for most people. Of course, that is still some way off: LuaTeX is scheduled to reach version 1.0 in 2012.
