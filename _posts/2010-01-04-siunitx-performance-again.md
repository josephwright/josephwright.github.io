---
title: siunitx performance (again)
layout: post
permalink: /2010/01/04/siunitx-performance-again/
categories:
  - Packages
  - siunitx
tags:
  - performance
---
My previous post mentioned some efforts to improve the performance of the [`siunitx`](https://ctan.org/pkg/siunitx) parser. I've now committed an entirely new version of the parsing code to the repository. For the interested reader, an [`siunitx` snapshot](/uploads/2010/01/siunitx.tds.zip) TDS-style `.zip` is available.

One thing that I find interesting in all of this is that even before optimising the code, version 2 still worked faster than version 1, even though it does more things. A lot of that is because the pre-built looping material in [`expl3`](https://ctan.org/pkg/expl3) does a much better job than my own attempts in version 1 of `siunitx`. Of course, good programmers will always use fast loops, but for the rest of us I think this shows how a sensible tool-kit can bring benefits 'behind the scenes'.
