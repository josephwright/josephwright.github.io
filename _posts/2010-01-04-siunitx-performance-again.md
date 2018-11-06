---
id: 596
title: siunitx performance (again)
date: 2010-01-04T19:48:39+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=596
permalink: /2010/01/04/siunitx-performance-again/
categories:
  - Packages
  - siunitx
tags:
  - performance
---
My previous post mentioned some efforts to improve the performance of the [siunitx](http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx) parser. I've now committed an entirely new version of the parsing code to the [repository](http://developer.berlios.de/projects/siunitx/). I've also done my best to speed up the rest of the package. The speed you see very much depends on the type of input involved. With my test file, I got a time of roughly 3 minutes using version 1 of siunitx, about 2 minutes before improving version 2, and about 1.5 minutes after. For comparison, doing no processing at all take the time down below 10 seconds for the same file (roughly 700 pages of repeated input). For the interested reader, an [siunitx snapshot](http://www.texdev.net/wp-content/uploads/2010/01/siunitx.tds_.zip) TDS-style zip is available.

One thing that I find interesting in all of this is that even before optimising the code, version 2 still worked faster than version 1, even though it does more things. A lot of that is because the pre-built looping material in [expl3](http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=expl3) does a much better job than my own attempts in version 1 of siunitx. Of course, good programmers will always use fast loops, but for the rest of us I think this shows how a sensible tool-kit can bring benefits “behind the scenes”.
