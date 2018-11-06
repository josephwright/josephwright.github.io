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
I've had a a few questions about the [achemso](https://ctan.org/pkg/achemso) bundle concerning creating references such as “Figures 1 to 3” automatically. The problem has been that I've been using the [varioref](https://ctan.org/pkg/varioref) package to turn `\ref{some-fig}` in “Figure 1” automatically, rather than having to put `Figure~\ref{some-fig}`. Unfortunately, varioref does not handle multiple references in an automated fashion.

For version 3.4 of achemso (which I've just sent to [CTAN](https://www.ctan.org)), I've switched to the [cleveref](https://ctan.org/pkg/cleveref) package. This means that you can now write something like `\ref{fig-1,fig-2,fig-3}` and get “Figures 1 to 3” without further effort. I hope that this makes life much easier for users, although it does mean that there is another package required to use achemso. I think that this is the right balance: I'm sure users will let me know if I've got it wrong.
