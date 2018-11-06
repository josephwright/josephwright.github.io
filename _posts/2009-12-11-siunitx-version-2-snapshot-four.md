---
id: 577
title: 'siunitx version 2: snapshot four'
date: 2009-12-11T07:03:28+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=577
permalink: /2009/12/11/siunitx-version-2-snapshot-four/
categories:
  - Packages
  - siunitx
tags:
  - snapshot
---
I'm continuing to work on version 2 of [siunitx](http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx), and the code has now reached the point where the basic macros (`\num`, `\SI`, `\si`, `\numrange` and `\SIrange`) work at least as well as the version one code. There are probably still some bugs, but I'm using the new code for my own work and at the moment all seems good. The internal improvements mean that while there are still things to add this should not be too hard.

If you want to try things out, as before you can grab things here:

- [The  source (dtx file)](http://www.texdev.net/wp-content/uploads/2009/12/siunitx.dtx)
- [The  documentation (pdf file)](http://www.texdev.net/wp-content/uploads/2009/12/siunitx.pdf)
- [The  extracted package (sty file)](http://www.texdev.net/wp-content/uploads/2009/12/siunitx.sty)
- [A  ready-to-install (tds) zip file](http://www.texdev.net/wp-content/uploads/2009/12/siunitx.tds_.zip)

What is on the list next is tackling the tables issues. That is going to be hard work, as there are some complicated things to sort out. So I will probably add a few bits and pieces to the rest of the code at the same time.

As always, feedback by [e-mail](mailto:joseph.wright@morningstar2.co.uk) or to the [BerliOS site](http://developer.berlios.de/projects/siunitx/) is very welcome.
