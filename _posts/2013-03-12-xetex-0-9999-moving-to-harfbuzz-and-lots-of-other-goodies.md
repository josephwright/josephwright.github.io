---
title: 'XeTeX 0.9999: Moving to HarfBuzz (and lots of other goodies)'
layout: post
permalink: /2013/03/12/xetex-0-9999-moving-to-harfbuzz-and-lots-of-other-goodies/
categories:
  - General
tags:
  - HarfBuzz
  - XeTeX
---
Khaled Hosny has announced on the [XeTeX mailing list](https://tug.org/mailman/listinfo/xetex) that XeTeX 0.9999 has just been released. The list of changes is pretty long, as XeTeX has had quite a backlog of issues. Probably the biggest single change is

>  Port OpenType layout from ICU LayoutEngine to HarfBuzz. HarfBuzz is actively maintained and generally have much wider support for
> OpenType spec, the switch fixes a number of OpenType bugs:
>  
> - Support version 2 OpenType Indic specs.
> - Many other Indic OpenType bugs, and support for the latest additions to OpenType spec.
> - Incorrect application of contextual features.
> - Incorrect kerning in fonts that has both old 'kern' table and new GPOS 'kern' feature.
> - Allow suppressing Latin ligatures with ZWNJ.
> - Support for variation selectors.
> - Support for user-specified features with complex scripts.

If you are familiar with layout engines, you'll know that while ICU has worked very well for XeTeX from day one, it's no longer being developed while [HarfBuzz](http://www.freedesktop.org/wiki/Software/HarfBuzz) is being developed. More importantly, HarfBuzz is supported by the open source community well beyond the TeX world, so by moving in this direction XeTeX gets the benefits of the efforts of many other people: part of the point of open source software. I'm sure it's been a _big_ effort making this change: I'm looking forward to testing it out.

The other headline change, at least for Mac users, is moving to Core Text rather than ATS/ATSUI. Apple have dropped support for the latter, so there was a worry about building XeTeX on the Mac in the future. That's now sorted, and means XeTeX should work as a 64-bit application on the Mac in future.

If you read the full announcement you'll see there are lots of other changes and bug fixes. Congratulations to Khaled on this: it's great to see that XeTeX continues to develop, and that several features have been added to make working with XeTeX and LuaTeX seamlessly are now there.
