---
id: 134
title: Babel woes
date: 2009-02-01T10:42:30+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=134
permalink: /2009/02/01/babel-woes/
categories:
  - Packages
  - siunitx
tags:
  - babel
  - UTF-8
---
I've had a couple of <a title="Multilingual support for Plain TeX or LaTeX." href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=babel">babel</a>-related bug reports for <a title="siunitx - A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a>.  The first was with the Spanish language option, where the <code>\percent</code> unit misbehaves as <code>\%</code> is redefined by babel. My fix for this has then caused a problem with the Italian language option, as it makes " an active character. So the latest release (v1.2d) fixes this too: apologies for the problems.

All of this makes more more eager than ever that a general move to UTF-8 input happens. This should cut down on the need for babel. At the same time, an updated LaTeX kernel (<a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a>) which includes more functionality would also help package authors know what to expect.
