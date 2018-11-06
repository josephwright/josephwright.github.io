---
title: Section numbers in achemso
layout: post
permalink: /2008/12/30/section-numbers-in-achemso/
categories:
  - achemso
  - Packages
---
When I wrote the [`achemso`](https://ctan.org/pkg/achemso) class for submissions to [American Chemical Society](http://www.acs.org) journals, I did my best to get the style of each journal correct. Of course, this is not easy as there are a lot of journals and they are not necessarily consistent in applying the style rules! One issue that comes up a lot is section numbering. Most of the journals do not number sections, most of the time. However, sometimes authors want to include section numbers. I need to look at this again for version 3.2, but in version 3.1 you need to do:

```latex
\makeatletter
\acs@restsecnums
\makeatother
```

somewhere in the preamble to restore numbering.
