---
id: 1423
title: Fixing problems the rapid way
date: 2012-08-24T09:27:25+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1423
permalink: /2012/08/24/fixing-problems-the-rapid-way/
categories:
  - LaTeX3
tags:
  - l3kernel
  - LuaTeX
  - unicode-math
---
The latest <a href="http://ctan.org/pkg/l3kernel"><code>l3kernel</code></a> update included a 'breaking change': something we know alters behaviour, but which is needed for the long term. Of course, despite the fact the team try to pick up what these things will break, we missed one, and there was an <a href="https://github.com/phst/lualatex-math/issues/4">issue with <code>lualatex-math</code></a> as a result, which <a href="https://github.com/wspr/unicode-math/issues/246">showed up for people using <code>unicode-math</code></a> (also <a href="http://tex.stackexchange.com/a/68552/73">reported on TeX-sx</a>). Luckily, those packages all use GitHub, as does the LaTeX3 team, so it was easy to quickly <a href="https://github.com/josephwright/lualatex-math">fork the code</a> and for me to create a fix. That's the big advantage of having code available using one of the distributed version systems (<a href="http://www.github.com">GitHub</a> and <a href="http://bitbucket.org">BitBucket</a> are the two obvious places): sending in a fix is a two-minute job, even if it's someone else's project. So I'd encourage everyone developing open code to got to <a href="http://www.ctan.org">CTAN</a> to consider using one of these services: it really does make fixing bugs easier. From report to fix and CTAN update in less than 24 h, which I'd say is pretty good!
