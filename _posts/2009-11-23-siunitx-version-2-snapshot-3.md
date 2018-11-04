---
id: 563
title: 'siunitx version 2: snapshot 3'
date: 2009-11-23T08:35:04+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=563
permalink: /2009/11/23/siunitx-version-2-snapshot-3/
categories:
  - Packages
  - siunitx
---
It's been a while since I gave an update on progress with <a title="A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> version 2. I've had other things on the go, but am trying to make some progress with the code as I have lots of bugs which are fixed in the new version. Since the last snapshot, I've gone back over everything and moved internally to <a title="An Experimental LaTeX3 Programming Convention" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=expl3">expl3</a> syntax. That makes my life a lot easier, as there are lots of tools available without needing to write them all for myself. It does mean that users/testers will need to have expl3 installed: you will need the most recent release, which should appear in <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> and <a title="MiKTeX Homepage" href="http://www.miktex.org/">MiKTeX</a> soon for online installation, or can be downloaded from <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a> (look for <a href="http://www.ctan.org/cgi-bin/filenameSearch.py?filename=expl3.tds.zip&amp;Search=Search">expl3.tds.zip</a>).

There are some notes and outstanding questions with the current snapshot: it is still some way from being finished. Things to be aware of or to think about:
<ul>
	<li>Places where units should be repeated are not working properly at the moment. That is the next thing I need to sort out: I'd hope it will be done soon (perhaps another snapshot in a couple of weeks)</li>
	<li>I'd set the defaults to use text mode for units and maths mode for numbers. This may not stay that way, see for example the results for <code>\SI{1.23}{J.mol^{-1}.K^{-1}}</code>. This is because printing units literally has to do the powers in the same font as the units.</li>
	<li>The options system is now using the LaTeX3 l3keys module. Following the pattern that looks likely for LaTeX3 work, I've given the options names divided into words using hyphens. I hope that they make sense.</li>
	<li>At present, complex numbers are always printed with the complex root (i) after the number. I need an option to reverse this, but can't think of a good name.</li>
	<li>I've tried to simplify the various ‘<code>trapambig…</code>’ options into a single one (<code>use-brackets</code>). I'm not sure if this will work for everyone: do people need the ability to turn bracketing on and off in a more granulated way?</li>
</ul>
For those who want to test things out, you can get:
<ul>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/11/siunitx.dtx">The source (dtx file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/11/siunitx.pdf">The documentation (pdf file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/11/siunitx.sty">The extracted package (sty file)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/11/siunitx.tds_.zip">A ready-to-install (tds) zip file</a></li>
</ul>