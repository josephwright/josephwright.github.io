---
title: 'Programming: Lua versus TeX'
layout: post
permalink: /2009/02/04/programming-lua-versus-tex/
categories:
  - General
tags:
  - ConTeXt
  - LuaTeX
---
As [LuaTeX](http://www.luatex.org/) progresses, the desire to use it in real documents increases.  [ConTeXt Mark IV](http://wiki.contextgarden.net/Mark_IV) is clearly the leading exponent of this, although it is still experimental and so perhaps not the best choice for day-to-day work. [Karl Berry](http://freefriends.org/~karl/) has said to me that he hopes that the inclusion of a “proper” programming language will bring new talent to (La)TeX. After all, some of the methods used to program TeX are complex to say the least.

This raises the question of how much to do in Lua and how much in TeX. Clearly, LuaTeX brings things to TeX that are impossible without it. So there it is simple: use Lua. However, what about things that can be done with either Lua or TeX? Part of this probably depends on the complexity of the different solutions (if it is easy in TeX, why do it in Lua, and _vice versa_). I'd also imagine that experiences TeX programmers will tend to stick to what they know, and favour TeX. On the other hand, new programmers coming to TeX because of Lua will favour the Lua route. I imagine that there will still be a lot more TeX than Lua code.
