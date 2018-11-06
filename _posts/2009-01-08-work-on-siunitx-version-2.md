---
id: 89
title: Work on siunitx version 2
date: 2009-01-08T08:10:43+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=89
permalink: /2009/01/08/work-on-siunitx-version-2/
categories:
  - Packages
  - siunitx
---
Progress on siunitx 2 was slower over Christmas than I'd hoped.  However, I should still manage a first snap-shot of what I'm doing some time this month.

I'm working on three different targets at once:

1. Making the existing code clearer. This means improving the internal naming of functions, making each section more independent of the others and trying to use some LaTeX3 ideas in the internal code. This is the fastest part of the job.
2. Improving the efficiency of the current code. LaTeX3 has lots of good ideas about loops and expandable tests, and I'm using this to make the existing code more efficient. I've removed a lot of loops from the current number parsing system, which makes for a faster package. Once everything works properly, I'll try to get some testing done on this to see what difference it makes.
3. Adding new features. This is the slowest job, unsurprisingly. There are various things I'm still working out how to do with numbers, before I even look at some of the unit-based problems.

Each of the areas takes time, and and have other things to do as well!  I'm still hoping to get something done in time for TeXlive 2009: it's always best to have some kind of target.
