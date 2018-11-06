---
id: 105
title: Units in ConTeXt
date: 2009-01-16T17:22:05+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=105
permalink: /2009/01/16/units-in-context/
categories:
  - Packages
  - siunitx
tags:
  - ConTeXt
  - units
---
Looking to gather ideas, I was looking at the <a title="ConTeXt Wiki" href="http://wiki.contextgarden.net">ConTeXt</a> “<a title="The ConTeXt units module" href="http://wiki.contextgarden.net/Units">units</a>” module. The approach taken there is to create free-standing macros, such as <code>\Second</code> or <code>\Candela</code>, and to use them to build up a string of units. Like some of the LaTeX solutions, this means that the user has to maunally include symbols (such as <code>\Times</code>) to get the formatting right. On the other hand, ConTeXt uses a glossary-like method for defining units (something I've thought about for <a title="siunitx - A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> in the past).  I'll certainly be thinking about something like that for siunitx version 2.
