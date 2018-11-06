---
id: 153
title: 'Programming: Lua versus TeX'
date: 2009-02-04T08:19:16+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=153
permalink: /2009/02/04/programming-lua-versus-tex/
categories:
  - General
tags:
  - ConTeXt
  - LuaTeX
---
As <a title="LuaTeX Homepage" href="http://www.luatex.org/">LuaTeX</a> progresses, the desire to use it in real documents increases.  <a title="ConTeXt Mark IV" href="http://wiki.contextgarden.net/Mark_IV">ConTeXt Mark IV</a> is clearly the leading exponent of this, although it is still experimental and so perhaps not the best choice for day-to-day work. <a title="Karl Berry's Homepage" href="http://freefriends.org/~karl/">Karl Berry</a> has said to me that he hopes that the inclusion of a “proper” programming language will bring new talent to (La)TeX. After all, some of the methods used to program TeX are complex to say the least.

This raises the question of how much to do in Lua and how much in TeX. Clearly, LuaTeX brings things to TeX that are impossible without it. So there it is simple: use Lua. However, what about things that can be done with either Lua or TeX? Part of this probably depends on the complexity of the different solutions (if it is easy in TeX, why do it in Lua, and <em>vice versa</em>). I'd also imagine that experiences TeX programmers will tend to stick to what they know, and favour TeX. On the other hand, new programmers coming to TeX because of Lua will favour the Lua route. I imagine that there will still be a lot more TeX than Lua code.
