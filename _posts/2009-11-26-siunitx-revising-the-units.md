---
title: siunitx: Revising the units
layout: post
permalink: /2009/11/26/siunitx-revising-the-units/
categories:
  - Packages
  - siunitx
---
Working on [`siunitx`](https://ctan.org/pkg/siunitx) version 2, I've been carefully back over the [SI units](http://www.bipm.org/en/si/si_brochure/). So the core code now defines everything that is listed in the various tables, plus `\percent` (seems pretty sensible) and the US spellings `\meter` and `\liter` (realism). Most of the units are easy enough to give a macro name to, but the speed of light (`\clight`) and reduced Planck constant (`\planckbar`) are possibly a bit odd. The minutes and seconds of arcs (`\arcminute` and `\arcsecond`) obviously need different names from the same units for time, and I hope make sense.

More awkward are the things beyond the SI units. I'm revising the abbreviations and so on, to bring more order to how everything is done. The real problems are the more specialist units that need to be defined (realism again), but that are clear non-SI. In my own area (chemistry) we tend to use 'molar' (moles per cubic decimetre) a lot, and so that is in. In the same way, there are some other areas that I've had good feedback on and know what is needed. However, there are also some odds and ends that I'm less sure on. High-energy physics seems to have a lot of units in the [`hepunits`](https://ctan.org/pkg/hepunits) package, but I don't know how many are really needed. Similarly, there are some older units for radiation does (roentgen's and rad's) that I don't really know what to do with.

I'm keen to get any ideas about the current direction. There will probably be another snapshot of the code and documentation in a couple of weeks, which will add a lot more of these awkward units. So take a look and make suggestions, either at the snapshots or at the development code.
