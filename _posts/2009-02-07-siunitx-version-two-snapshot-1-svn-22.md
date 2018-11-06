---
id: 162
title: 'siunitx version two: Snapshot 1 (SVN 22)'
date: 2009-02-07T20:02:32+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=162
permalink: /2009/02/07/siunitx-version-two-snapshot-1-svn-22/
categories:
  - Packages
  - siunitx
---
As promised a while ago, I've been working to get a snapshot of my work on <a title="siunitx version 2" href="http://siunitx.berlios.de">siunitx version 2</a> ready. I've now got something that works “as far as it goes”, so I'm making a first snapshot available.  This is version control (SVN) repository revision 22, which you can see on <a title="BerliOS" href="http://www.berlios.de">BerliOS</a>. As this is a very earlier version of what I'm looking at, I'm just posting three files here:
<ul>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/02/siunitx.dtx">The source (.dtx)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/02/siunitx.pdf">The user manual (.pdf)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/02/siunitx.sty">The style file (.sty)</a></li>
</ul>
Currently, only the <code>\num</code> macro works at all, and even then only for single numbers. However, there are several points to note for testers  and interested users:
<ol>
	<li>The package understands complex numbers.</li>
	<li>The options use <a title="The pgf and Tikz bundle" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=pgf">pgfkeys</a>, although this may change.</li>
	<li>Input and output of numbers are much more clearly separated, which makes extension much easier.</li>
	<li>A number of subtle bugs in version one are fixed here. (No-one else seems to have noticed them, so for the moment I've not fixed them in the release version!)</li>
	<li>Currently, only the new options are implemented, although before release the full set of version one options will be implemented.</li>
</ol>
Although the snapshot is not functional enough for general use, I'd appreciate any feedback people can give.  There are probably some bugs in the number code, which obviously I'd like to hear about.  The new option arrangement is something I'd like to get opinions on.  I feel it is much more logical (and easier to extend as new ideas arrive), but I'm obviously keen to see how others see it.
