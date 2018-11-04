---
id: 2274
title: 'LaTeX2e: UTF-8 as standard'
date: 2018-03-25T13:59:30+00:00
author: josephwright
layout: post
guid: https://www.texdev.net/?p=2274
permalink: /2018/03/25/latex2e-utf-8-as-standard/
categories:
  - General
tags:
  - LaTeX kernel
  - Unicode
  - UTF-8
---
Stability is a key idea when making changes to the LaTeX2e kernel: users need to know that they'll always get the same output for the same (valid) input. At the same time, the world moves on and we need to respond to real-world use. To date, the LaTeX kernel has stuck to purely 'classical' 7-bit input support 'out of the box', meaning that with pdfTeX you need to load `inputenc` to properly use any extended characters. For English speakers that doesn't really show up, but almost everyone else needs

    \usepackage[<encoding>]{inputenc}

at least unless they are using XeTeX or LuaTeX. When there were many competing input encodings, having to load one specifically made more sense, but today UTF-8 is _the_ standard, and (almost) all new documents should be using it.

For the next LaTeX2e release, the team are changing this position, and UTF-8 will be understood as default: https://github.com/latex3/latex2e/issues/24. For most users, this will be entirely transparent: they'll already be using `inputenc`. Of course, there will be a few users who need to make adjustments, most obviously those who have relied on the default settings for the upper-half of the 8-bit range (they will need `\usepackage[latin1]{inputenc}`).

Testing is underway and a few areas are still being addressed. The aim is to make life easier for all LaTeX users: feedback is most welcome.