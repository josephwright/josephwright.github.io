---
id: 826
title: Testing versions of siunitx v2.1 on TLcontrib
date: 2010-10-12T19:41:02+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=826
permalink: /2010/10/12/testing-versions-of-siunitx-v2-1-on-tlcontrib/
categories:
  - Packages
  - siunitx
tags:
  - TLcontrib
---
I'm working on the <a href="http://bitbucket.org/josephwright/siunitx/issues?status=new&amp;status=open&amp;milestone=v2.1">list of issues</a> for <a title="A comprehensvie (SI) units package" href="http://ctan.org/pkg/siunitx">siunitx</a> v2.1. As I do, I hope that the code is staying usable at all times! The list is getting shorter (finally), so I'm hoping to get something released around the end of the month.  One thing that I need for that is testing. My <a title="TeX Live packaging expands" href="http://www.texdev.net/2010/10/09/tex-live-packaging-expands/">recent post about TLcontrib</a> mentioned this as a route for testing packages prior to release. So I'm taking advantage, and sending snapshots of siunitx to TLcontrib each time I add a new feature. So if you want to help to test things out, then you can run
<pre>tlmgr --repository http://tlcontrib.metatex.org/2010 update siunitx</pre>
from your command prompt/terminal. Let me know about any new issues!