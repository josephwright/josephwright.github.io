---
id: 285
title: Supporting Windows users
date: 2009-05-07T07:23:32+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=285
permalink: /2009/05/07/supporting-windows-users/
categories:
  - General
---
Many “open” projects are developed mainly by people using Unix-based operating systems (Linus, MacOS X, OpenBSD, <em>etc.</em>). This sometimes leads to a rather awkward situation for Windows users. Many of the tools that are assumed to be available (GCC, make, grep, …) simply are not. TeX is luckily cross-platform, and recent versions of <a title="TeX Live" href="http://www.tug.org/texlive">TeX Live</a> work hard to work on Windows as well as on *nix systems. However, that can still leave a few issues.The <a title="LaTeX3 development code" href="http://www.latex-project.org/code.html">LaTeX3 experimental code</a> has a series of test files, make scripts and so on, to aid development. However, these only work if things like make and bash are actually available. So I've recently added a set of batch files to the source store, which hopefully do basically the same thing but using Windows tools. I've had to require <a title="The Perl Directory" href="http://www.perl.org">Perl</a> for the test scripts, as these need to be parsed and re-formatted. The batch files also need a command-line zip program: I tend to use <a title="7-Zip" href="http://www.7zip.org">7-Zip</a>. Hopefully, though, these are not too much to ask for!

In the longer term, <a title="LuaTeX Homepage" href="http://www.luatex.org">LuaTeX</a> should mean that auxiliary stuff can be done using Lua, as it will be available cross-platform. However, it could be many years before we reach that state!
