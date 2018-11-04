---
id: 120
title: siunitx version 1.2
date: 2009-01-22T13:32:22+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=120
permalink: /2009/01/22/siunitx-version-12/
categories:
  - Packages
  - siunitx
---
I've just uploaded <a title="siunitx - A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> version 1.2 to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a>.  This adds the macros <code>\numrange</code> and <code>\SIrange</code> to the package, so that you can write <code>\SIrange{1}{10}{\second}</code> and get out “1 s to 10 s” (or the less correct “1 to 10 s”, if you want).