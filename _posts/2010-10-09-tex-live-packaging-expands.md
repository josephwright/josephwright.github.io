---
id: 823
title: TeX Live packaging expands
date: 2010-10-09T10:41:00+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=823
permalink: /2010/10/09/tex-live-packaging-expands/
categories:
  - General
tags:
  - TeX Live
---
Taco Hoekwater [announced yesterday](https://tug.org/pipermail/tex-live/2010-October/027486.html) that he's set up a new TeX Live package repository, [TLcontrib](http://tlcontrib.metatex.org/). The idea is that this can be used as a parallel source to the ‘normal’ TeX Live repositories, to hold things which can't go into TeX Live (license issues), binary updates, testing versions of packages and so on. It's early days, but the idea looks good to me. I'm planning to use this mechanism for making pre-release versions of [`siunitx`](https://ctan.org/pkg/siunitx) available. At the same time, I think I'll be encouraging the [LaTeX3 Project](https://www.latex-project.org/latex3.html) to use this method for testing snapshots of [`expl3`](https://ctan.org/pkg/expl3). The advantage of this is that only people who really want to test out new material will get it, enabling more testing before [CTAN](https://www.ctan.org) releases.

Of course, this only affects TeX Live users: [MiKTeX](https://www.miktex.org/) is not affected at all. I'm hoping that enough TeX Live users will be interested in the idea to enable a community of ‘test volunteers’ to develop.
