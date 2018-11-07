---
title: Supporting Windows users
layout: post
permalink: /2009/05/07/supporting-windows-users/
categories:
  - General
---
Many 'open' projects are developed mainly by people using Unix-based operating systems (Linus, MacOS X, OpenBSD, _etc._). This sometimes leads to a rather awkward situation for Windows users. Many of the tools that are assumed to be available (GCC, `make`, `grep`, …) simply are not. TeX is luckily cross-platform, and recent versions of [TeX Live](https://tug.org/texlive) work hard to work on Windows as well as on *nix systems. However, that can still leave a few issues.The [LaTeX3 experimental code](https://www.latex-project.org/code.html) has a series of test files, make scripts and so on, to aid development. However, these only work if things like make and bash are actually available. So I've recently added a set of batch files to the source store, which hopefully do basically the same thing but using Windows tools. I've had to require [Perl](http://www.perl.org) for the test scripts, as these need to be parsed and re-formatted. The batch files also need a command-line zip program: I tend to use [7-Zip](http://www.7zip.org). Hopefully, though, these are not too much to ask for!

In the longer term, [LuaTeX](http://www.luatex.org) should mean that auxiliary stuff can be done using Lua, as it will be available cross-platform. However, it could be many years before we reach that state!
