---
id: 693
title: TeX Live 2009 on Ubuntu 10.04 (Lucid Lynx)
date: 2010-05-06T19:32:02+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=693
permalink: /2010/05/06/tex-live-2009-on-ubuntu-10-04-lucid-lynx/
categories:
  - General
tags:
  - TeX Live
  - Ubuntu
---
TeX users on Linux tend to use the packaged TeX installation provided by there distro, rather than using the standard <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> installer and managing things themselves. <a title="Ubuntu" href="http://www.ubuntu.com/">Ubuntu</a> is one of the more popular Linux distros, and there has been an issue for a while that they had stuck with TeX Live 2007, despite TeX Live 2008 and then TeX Live 2009 being released.

The latest Ubuntu release, 10.04 ‘Lucid Lynx’, finally moves to TeX Live 2009. This finally makes it easy to get TeX Live in a reasonable up to date version:
<pre>sudo apt-get install texlive
</pre>
This grabs a subset of the complete TeX Live 2009, but seems to include quite a good selection (a bit like the <a title="MiKTeX" href="http://www.miktex.org/">MiKTeX</a> basic installation on Windows, but I think a bit bigger). TeXworks is also on the list (at least the stable version), so if you don't want to compile it from the source you can do
<pre>sudo apt-get install texworks</pre>
and be ready to go. Of course, you might still need to grab a few more bits of TeX Live (for example, <a title="XeTeX" href="http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=xetex">XeTeX</a> is not included in the standard selection). However, it's definitely an improvement of the earlier situation.
