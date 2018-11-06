---
id: 91
title: 'siunitx 2: more numbers, more tables, SVN?'
date: 2009-01-10T18:20:24+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=91
permalink: /2009/01/10/siunitx-2-more-numbers-more-tables-svn/
categories:
  - Packages
  - siunitx
---
The issue of input formats for <a title="siunitx - A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> and numbers has <a href="http://www.texdev.net/2008/12/21/developement-timetables/#comments">been mentioned</a>.  It seems every time I think I've sorted broadly what I need to do, other ideas come up.  I've thought about scientific notation before, but haven't had a go at coding anything.  The idea of “compressing” error input such as <code>1.23\pm 0.02</code> into 1.23(2) was mentioned to me before, but that one slipped off my radar.  I guess I should re-visit both of these areas and see what I can do.  Of course, that will delay me with other things, but I'd really like <a title="siunitx version 2" href="http://siunitx.berlios.de">siunitx 2</a> to cover a lot of things that version 1 does less well.

Tables have also been raised (again).  I've had a quick look at <a title="pgfplots, which includes pgfplotstable" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=pgfplots">pgfplotstable</a> in the past, but I suppose I should read things in detail.  I mention it a lot,  but tables were not on the original “manifesto” for siunitx, and have rather crept up on me.  It seems that this is a key area for users, and so I'll also need to look at this area again.  I've already said I need to work on more table ideas, so this is not really that much of a surprise. Over all, my aims in siunitx are probably slightly different to pgfplotstable, but I'll see what I can learn.

All of this leads me to worrying about public information and releases. As a developer, I'd love to keep things simple for users, and only release working material. On the other hand, advanced users often provide good feedback well before things are done. I think I need some kind of public repository for the version 2 code, and as I currently use <a href="http://www.berlios.de">BerliOS</a> for my LaTeX3 ideas, I'll look at settings something up there over the weekend. They seem to be quite happy with the <a title="LaTeX Projecy Public License" href="http://www.latex-project.org/lppl/">LPPL</a>, which not every free open-source hosting service is.
