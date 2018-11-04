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
I'm continuing to work on version 2 of <a title="A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a>, and the code has now reached the point where the basic macros (<code>\num</code>, <code>\SI</code>, <code>\si</code>, <code>\numrange</code> and <code>\SIrange</code>) work at least as well as the version one code. There are probably still some bugs, but I'm using the new code for my own work and at the moment all seems good. The internal improvements mean that while there are still things to add this should not be too hard.

If you want to try things out, as before you can grab things here:
<ul>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/12/siunitx.dtx">The  source (dtx file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/12/siunitx.pdf">The  documentation (pdf file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/12/siunitx.sty">The  extracted package (sty file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/12/siunitx.tds_.zip">A  ready-to-install (tds) zip file</a></li>
</ul>
What is on the list next is tackling the tables issues. That is going to be hard work, as there are some complicated things to sort out. So I will probably add a few bits and pieces to the rest of the code at the same time.

As always, feedback by <a href="mailto:joseph.wright@morningstar2.co.uk">e-mail</a> or to the <a href="http://developer.berlios.de/projects/siunitx/">BerliOS site</a> is very welcome.