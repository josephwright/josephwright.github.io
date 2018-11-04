---
id: 243
title: 'siunitx version two: Snapshot 2 (SVN 62)'
date: 2009-03-29T21:39:58+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=243
permalink: /2009/03/29/siunitx-version-two-snapshot-2-svn-62/
categories:
  - Packages
  - siunitx
---
As promised, a second snapshot of siunitx version 2 is now available:
<ul>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/03/siunitx.dtx">The source  (.dtx)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/03/siunitx.pdf">The user manual (.pdf)</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2009/03/siunitx.sty">The style file  (.sty)</a></li>
</ul>
This adds functioning unit processing to the test code, as well as sorting bugs in the previous snaphot (for example, a few problems with numbers). Testers will see that version 2 will provide a lot more units by default: this is a result of changing the method for defining units, making it much easier to avoid clashes with other packages. As with snapshot one, there are a lot of gaps in the existing code (for example, backward-compatibilty!). Feedback is very welcome.