---
id: 338
title: Progress on siunitx version 2
date: 2009-07-03T07:19:53+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=338
permalink: /2009/07/03/progress-on-siunitx-version-2/
categories:
  - LaTeX3
  - Packages
  - siunitx
---
I've been doing quite a bit of thinking about <a href="http://github.com/josephwright/siunitx">siunitx version 2</a>. My original plan was to write everything in standard LaTeX2e code, but the more I thought about things the more it has not looked like such a good idea. siunitx needs a lot of programming tools, and these are almost all available in the experimental <a title="LaTeX Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> code which is now approaching stability. At the same time, there are still some difficult issues to solve for siunitx, and I'm going to need some more support stuff, I think. So I've revised my ideas on how to progress.

Currently, I'm moving the code I have already re-written to use LaTeX3 conventions internally. I'm then going to try to solve the remaining issues for version 2. The aim is to have a package which will run on LaTeX2e, using LaTeX3 internals, so that I can eventually create a LaTeX3-only edition with the same interface ideas. I'm going to try to crack on with things, but it will take a while to solve the remaining issues!
