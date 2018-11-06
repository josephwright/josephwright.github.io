---
title: Fixing problems the rapid way
layout: post
permalink: /2012/08/24/fixing-problems-the-rapid-way/
categories:
  - LaTeX3
tags:
  - l3kernel
  - LuaTeX
  - unicode-math
---
The latest [`l3kernel`](https://ctan.org/pkg/l3kernel) update included a 'breaking change': something we know alters behaviour, but which is needed for the long term. Of course, despite the fact the team try to pick up what these things will break, we missed one, and there was an [issue with `lualatex-math`](https://github.com/phst/lualatex-math/issues/4) as a result, which [showed up for people using `unicode-math`](https://github.com/wspr/unicode-math/issues/246) (also [reported on TeX-sx](https://tex.stackexchange.com/a/68552/73)). Luckily, those packages all use GitHub, as does the LaTeX3 team, so it was easy to quickly [fork the code](https://github.com/josephwright/lualatex-math) and for me to create a fix. That's the big advantage of having code available using one of the distributed version systems ([GitHub](http://www.github.com) and [BitBucket](https://bitbucket.org) are the two obvious places): sending in a fix is a two-minute job, even if it's someone else's project. So I'd encourage everyone developing open code to got to [CTAN](https://www.ctan.org) to consider using one of these services: it really does make fixing bugs easier. From report to fix and CTAN update in less than 24 h, which I'd say is pretty good!
