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
Having <a href="http://www.texdev.net/2009/10/06/what-does-write18-mean/">posted</a> about restricted <code>\write18</code> support in <a title="TeX Live" href="http://www.tug.org/texlive">TeX Live</a> 2009 (and <a title="MiKTeX Homepage" href="http://www.miktex.org/">MiKTeX </a>2.8), a message to the TeX Live mailing list now tells me that for the moment there's been a change:
<blockquote>… we pulled the plug and try to fix it. The problem is that
allowing epstopdf we in fact obliterate openout_any becasue
epstopdf can write everywhere.
As long as we are not able to provide a restricted epstopdf that
only allows writing to subdirectories or similar we will
unfortunately not have this feature …</blockquote>
So for the moment you still need to turn on <code>\write18</code> explicitly if you need it (at least with TeX Live: I'd imagine that MiKTeX will be updated with the same change). I hope that a solution can be found to provide easy to use <code>\write18</code> for a subset of ‘safe’ programs, but for the moment we have to wait.