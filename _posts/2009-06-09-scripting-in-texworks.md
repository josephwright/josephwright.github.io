---
title: Scripting in TeXworks
layout: post
permalink: /2009/06/09/scripting-in-texworks/
categories:
  - TeXworks
tags:
  - Lua
---
Stefan Löffler has recently posted to the [TeXworks mailing list](https://tug.org/pipermail/texworks/) that he's sorted out a patch to integrate [Lua](https://www.lua.org) into [TeXworks](https://tug.org/texworks/). Many people will be aware that Lua is very much the scripting language of the moment in the TeX world, because of the [LuaTeX](http://www.luatex.org) project. So it makes sense to consider it as a method for scripting TeXworks. The idea has always been that TeXworks will have a simple interface but powerful features available to those who want them. So adding scripting is a vital step forward. With a light-weight scripting system available, power users can code their own features into TeXworks while leaving the basics accessible to everyone.

That doesn't mean that Lua has to be the (only) language available: Jonathan Kew (TeXworks lead developer) has suggested [QtScript](http://doc.trolltech.com/4.3/qtscript.html) (which is JavaScript-like) as a possibility. TeXworks is built using [Qt](http://www.qtsoftware.com/), so there is a definite logic here. As Jonathan himself points out, actually having a patch available certainly means that Lua is likely to be integrated!
