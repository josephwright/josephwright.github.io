---
id: 589
title: 'siunitx: Getting the micro symbol right'
date: 2009-12-22T21:12:47+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=589
permalink: /2009/12/22/siunitx-getting-the-micro-symbol-right/
categories:
  - Packages
  - siunitx
tags:
  - micro
  - XeTeX
---
I get a few e-mails about <a title="A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> and the micro symbol. People tend to be surprised that the symbol ‘sticks’ to a look very much like Computer Modern. The reason is that picking a proper upright (not italic) μ is not so easy in TeX. You don't get one in Computer Modern, so siunitx takes one from the TS1 (text support) set in the absence of a better plan. I've set up some auto-detection for a few obvious alternatives (such as the <a title="Upright Greek letters" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=upgreek">upgreek</a> package), but that doesn't really work for <a title="The XeTeX Typesetting System" href="http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=XeTeX">XeTeX</a> users.

XeTeX users are likely to load system fonts, and I'd hope be using UTF-8 input. That makes it hard to auto-detect what they are doing, but should make life easier for them to get things right. A lot of more comprehensive fonts include Greek letters in the main font, so getting the μ right is simple:
<pre>\sisetup{
  mathsmu = \text{μ},
  textmu  = μ
}
</pre>
or for people testing <a href="http://developer.berlios.de/projects/siunitx/">version 2 of siunitx</a>:
<pre>\sisetup{
  maths-micro = \text{μ},
  text-micro  = μ
}
</pre>
There may be a bit of testing required: this will not work if, for example, you are using the Latin Modern font.
