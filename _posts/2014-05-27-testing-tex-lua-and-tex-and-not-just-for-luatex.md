---
title: Testing TeX&#58; Lua and TeX, and not just for LuaTeX
layout: post
permalink: /2014/05/27/testing-tex-lua-and-tex-and-not-just-for-luatex/
categories:
  - LaTeX3
---
I [wrote recently](/2014/05/25/lua-for-latex3-build-scripts/) about the LaTeX3 build scripts, and that we are moving them to Lua for cross-platform work. One particular area the team are interested in is 'unit testing', something that's common in 'real' programming but not so widespread for (La)TeX. The main reason for that is obvious: most people programming TeX aren't professionals but instead do it as an add-on to their 'real' jobs (in my case, chemistry).

The LaTeX3 team have had unit tests for LaTeX for many years. The way these work is quite simple. First, set up a TeX run which does whatever tests are needed and write the output to the log file. The raw logs tend to be rather long, and have information in that varies from system to system, so the second stage is to run a script to extract out just the 'important' parts of the log (those get marked up by the TeX set up). The 'processed' log can then be compared to one prepared in a 'reference' run (where someone has checked the results by hand): if the two results match, the test passes.

Up to now, we've used Perl for that 'log processing' and have only run tests using pdfTeX. Moving to Lua for our scripting, we can drop Perl and do the post-processing in the build scripts themselves. That makes almost everything self-contained: other than needing Info-ZIP for making CTAN release zip files, all that is needed is a TeX system (featuring LuaTeX for `texlua`) and the operating system itself (basic file operations but also `diff`/`fc`). At the same time, we're expanding our tests to run them with pdfTeX, XeTeX and LuaTeX. That's already thrown up several bugs in LuaTeX: nothing most people will notice most of the time, but reported to the developers and to be fixed. (Most of these are about formatting in the log: if you test based on log changes, these are important!)

While the scripts aren't fully 'portable' as they are designed around our development set up, the structures should be pretty clear. The LaTeX test script is also quite general. So we'd like to hope that other people can adopt and adapt them: feedback always very welcome!
