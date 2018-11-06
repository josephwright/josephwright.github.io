---
id: 215
title: Change for the better
date: 2009-03-05T19:50:43+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=215
permalink: /2009/03/05/change-for-the-better/
categories:
  - General
tags:
  - BibTeX
  - graphicx
  - LaTeX community
  - natbib
---
There have been a couple of discussions recently, both concerned with “change for the better”. The first, on the[ LaTeX-L list](http://news.gmane.org/gmane.comp.tex.latex.latex3/), is about adding the ability to convert EPS graphics to PDF “on the fly”.  The suggestion is to have the graphicx package load epstopdf automatically, and to arrange a limited version of `\write18` that will only allow known commands to be run. That should let ordinary users include EPS files with pdfLaTeX without needing to worry about the detail.  A good thing, but it does raise one issue.  People who use updated versions of LaTeX will have this feature, but if they send their files to others who don't, things won't “just work”.  This can't really be avoided: if you add a new feature, then people without the update get a different result from those who do have it. Not much you can do, if you want any change at all!

The second change has come up on the [LaTeX Community](http://www.latex-community.org/) and [comp.text.tex](http://groups.google.com/group/comp.text.tex/topics). The latest version of [natbib](https://ctan.org/pkg/natbib) is rather more careful than earlier versions about the BibTeX style file used. This means that the latest version gives an error, where older versions silently change settings to “mind-read” what the user wants. This has lead to a lot of confusion, and some people recommending replacing the newer version with the old one! In the end, the change here is also for the better: the error that is causing problems (where the BibTeX style needs the “numbers” option, and it's not been given) is perfectly sensible. But it also shows the dangers of mending or improving things: people get used to the sub-optimal behaviour, and think something is wrong when it is sorted out!

Conclusion: make change for the better, but be ready for complaints.
