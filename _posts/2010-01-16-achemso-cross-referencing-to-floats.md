---
id: 606
title: 'achemso: Cross-referencing to floats'
date: 2010-01-16T09:55:49+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=606
permalink: /2010/01/16/achemso-cross-referencing-to-floats/
categories:
  - achemso
  - Packages
tags:
  - cleveref
---
I've had a a few questions about the <a title="Support for American Chemical Society journal submissions" href="http://ctan.org/pkg/achemso">achemso</a> bundle concerning creating references such as “Figures 1 to 3” automatically. The problem has been that I've been using the <a title="Intelligent page references" href="http://ctan.org/pkg/varioref">varioref</a> package to turn <code>\ref{some-fig}</code> in “Figure 1” automatically, rather than having to put <code>Figure~\ref{some-fig}</code>. Unfortunately, varioref does not handle multiple references in an automated fashion.

For version 3.4 of achemso (which I've just sent to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a>), I've switched to the <a title="Automatic cross-reference formatting" href="http://ctan.org/pkg/cleveref">cleveref</a> package. This means that you can now write something like <code>\ref{fig-1,fig-2,fig-3}</code> and get “Figures 1 to 3” without further effort. I hope that this makes life much easier for users, although it does mean that there is another package required to use achemso. I think that this is the right balance: I'm sure users will let me know if I've got it wrong.
