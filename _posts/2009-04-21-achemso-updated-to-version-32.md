---
title: achemso updated to version 3.2
layout: post
permalink: /2009/04/21/achemso-updated-to-version-32/
categories:
  - achemso
  - Packages
---
I've just uploaded version 3.2 of [`achemso`](https://ctan.org/pkg/achemso) to [CTAN](https://www.ctan.org), and also sent it off the [American Chemical Society](http://www.acs.org). The development for v3.2 has mainly been about making using the package easier for end users. I've removed a lot of dependency on other support packages, so that it only uses very standard LaTeX packages (things like [`float`](https://ctan.org/pkg/float) and [`caption`](https://ctan.org/pkg/caption)). I've also made the package cope better with older versions of [`xkeyval`](https://ctan.org/pkg/xkeyval), by using only a subset of the functions provided there. There are a few bug fixes as well, plus a new environment for graphic TOC entries. Hopefully, this makes life easier for manuscript authors.
