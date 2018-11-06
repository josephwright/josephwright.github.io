---
id: 1042
title: Updating LaTeX3 support in MiKTeX
date: 2011-07-12T19:59:34+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1042
permalink: /2011/07/12/updating-latex3-support-in-miktex/
categories:
  - LaTeX3
tags:
  - MiKTeX
---
The LaTeX3 Project have recently updated the organisation of the various LaTeX3-based packages on CTAN. This means that the older expl3 and xpackages need to be replaced by <a href="http://ctan.org/pkg/l3kernel">l3kernel</a> and <a href="http://ctan.org/pkg/l3packages">l3packages</a>. Unfortunately, this seems to <a href="http://www.latex-community.org/forum/viewtopic.php?f=9&amp;t=14110">confuse MiKTeX</a>, which does not pick up the need to install the new material. So MiKTeX users will need to do this by hand in the MiKTeX Package Manager. This should be a passing problem, but does seem to be causing some confusion for MiKTeX users.
