---
id: 499
title: No restricted \write18 just yet!
date: 2009-10-14T17:05:10+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=499
permalink: /2009/10/14/no-restricted-write18-just-yet/
categories:
  - General
---
Having [posted](http://www.texdev.net/2009/10/06/what-does-write18-mean/) about restricted `\write18` support in [TeX Live](http://www.tug.org/texlive) 2009 (and [MiKTeX ](http://www.miktex.org/)2.8), a message to the TeX Live mailing list now tells me that for the moment there's been a change:

> … we pulled the plug and try to fix it. The problem is that
allowing epstopdf we in fact obliterate openout_any becasue
epstopdf can write everywhere.
As long as we are not able to provide a restricted epstopdf that
only allows writing to subdirectories or similar we will
unfortunately not have this feature …

So for the moment you still need to turn on `\write18` explicitly if you need it (at least with TeX Live: I'd imagine that MiKTeX will be updated with the same change). I hope that a solution can be found to provide easy to use `\write18` for a subset of ‘safe’ programs, but for the moment we have to wait.
