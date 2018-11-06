---
title: Updating LaTeX3 support in MiKTeX
layout: post
permalink: /2011/07/12/updating-latex3-support-in-miktex/
categories:
  - LaTeX3
tags:
  - MiKTeX
---
The LaTeX3 Project have recently updated the organisation of the various LaTeX3-based packages on CTAN. This means that the older expl3 and xpackages need to be replaced by [`l3kernel`](https://ctan.org/pkg/l3kernel) and [`l3packages`](https://ctan.org/pkg/l3packages). Unfortunately, this seems to [confuse MiKTeX](http://www.latex-community.org/forum/viewtopic.php?f=9&amp;t=14110), which does not pick up the need to install the new material. So MiKTeX users will need to do this by hand in the MiKTeX Package Manager. This should be a passing problem, but does seem to be causing some confusion for MiKTeX users.
