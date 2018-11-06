---
id: 307
title: Scripting in TeXworks
date: 2009-06-09T10:08:03+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=307
permalink: /2009/06/09/scripting-in-texworks/
categories:
  - TeXworks
tags:
  - Lua
---
Stefan Löffler has recently posted to the <a title="The texworks Archives" href="http://tug.org/pipermail/texworks/">TeXworks mailing list</a> that he's sorted out a patch to integrate <a title="The Programming Language Lua" href="http://www.lua.org">Lua</a> into <a title="TeXworks: lowering the entry barrier to the TeX world" href="http://tug.org/texworks/">TeXworks</a>. Many people will be aware that Lua is very much the scripting language of the moment in the TeX world, because of the <a title="LuaTeX Homepage" href="http://www.luatex.org">LuaTeX</a> project. So it makes sense to consider it as a method for scripting TeXworks. The idea has always been that TeXworks will have a simple interface but powerful features available to those who want them. So adding scripting is a vital step forward. With a light-weight scripting system available, power users can code their own features into TeXworks while leaving the basics accessible to everyone.

That doesn't mean that Lua has to be the (only) language available: Jonathan Kew (TeXworks lead developer) has suggested <a title="QtScript Module" href="http://doc.trolltech.com/4.3/qtscript.html">QtScript</a> (which is JavaScript-like) as a possibility. TeXworks is built using <a title="Qt - A cross-platform application and UI framework" href="http://www.qtsoftware.com/">Qt</a>, so there is a definite logic here. As Jonathan himself points out, actually having a patch available certainly means that Lua is likely to be integrated!
