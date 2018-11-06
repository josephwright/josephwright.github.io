---
id: 55
title: Section numbers in achemso
date: 2008-12-30T09:53:06+00:00
author: josephwright
layout: post
guid: http://texdev.wordpress.com/?p=55
permalink: /2008/12/30/section-numbers-in-achemso/
categories:
  - achemso
  - Packages
---
When I wrote the <a title="The achemso bundle" href="http://ctan.org/pkg/achemso">achemso</a> class for submissions to <a title="The American Chemical Society" href="http://www.acs.org">American Chemical Society</a> journals, I did my best to get the style of each journal correct. Of course, this is not easy as there are a lot of journals and they are not necessarily consistent in applying the style rules! One issue that comes up a lot is section numbering. Most of the journals do not number sections, most of the time. However, sometimes authors want to include section numbers. I need to look at this again for version 3.2, but in version 3.1 you need to do:

<pre>\makeatletter
\acs@restsecnums
\makeatother</pre>

somewhere in the preamble to restore numbering.
