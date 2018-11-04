---
id: 1609
title: 'XeTeX 0.9999: Moving to HarfBuzz (and lots of other goodies)'
date: 2013-03-12T09:01:20+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1609
permalink: /2013/03/12/xetex-0-9999-moving-to-harfbuzz-and-lots-of-other-goodies/
categories:
  - General
tags:
  - HarfBuzz
  - XeTeX
---
<p>Khaled Hosny has announced on the <a href="http://tug.org/mailman/listinfo/xetex">XeTeX mailing list</a> that XeTeX 0.9999 has just been released. The list of changes is pretty long, as XeTeX has had quite a backlog of issues. Probably the biggest single change is</p>

<blockquote>
  <p>Port OpenType layout from ICU LayoutEngine to HarfBuzz. HarfBuzz is actively maintained and generally have much wider support for<br>OpenType spec, the switch fixes a number of OpenType bugs:</p>
  
  <ul>
  <li>Support version 2 OpenType Indic specs.</li>
  <li>Many other Indic OpenType bugs, and support for the latest additions to OpenType spec.</li>
  <li>Incorrect application of contextual features.</li>
  <li>Incorrect kerning in fonts that has both old “kern” table and new GPOS “kern” feature.</li>
  <li>Allow suppressing Latin ligatures with ZWNJ.</li>
  <li>Support for variation selectors.</li>
  <li>Support for user-specified features with complex scripts.</li>
  </ul>
</blockquote>

<p>If you are familiar with layout engines, you'll know that while ICU has worked very well for XeTeX from day one, it's no longer being developed while <a href="http://www.freedesktop.org/wiki/Software/HarfBuzz">HarfBuzz</a> is being developed. More importantly, HarfBuzz is supported by the open source community well beyond the TeX world, so by moving in this direction XeTeX gets the benefits of the efforts of many other people: part of the point of open source software. I'm sure it's been a <em>big</em> effort making this change: I'm looking forward to testing it out.</p>

<p>The other headline change, at least for Mac users, is moving to Core Text rather than ATS/ATSUI. Apple have dropped support for the latter, so there was a worry about building XeTeX on the Mac in the future. That's now sorted, and means XeTeX should work as a 64-bit application on the Mac in future.</p>

<p>If you read the full announcement you'll see there are lots of other changes and bug fixes. Congratulations to Khaled on this: it's great to see that XeTeX continues to develop, and that several features have been added to make working with XeTeX and LuaTeX seamlessly are now there.</p>
