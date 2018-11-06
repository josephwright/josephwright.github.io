---
id: 209
title: Too much information!
date: 2009-02-26T19:36:12+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=209
permalink: /2009/02/26/too-much-information/
categories:
  - LaTeX3
tags:
  - log messages
---
A recent announcement on [comp.text.tex](http://groups.google.com/group/comp.text.tex/topics) for a new package, [`silence`](https://ctan.org/pkg/silence), coincides with some discussion in the [LaTeX3](http://www.latex-project.org/latex3.html) team about how to handle messages for the user. The LaTeX3 stuff is currently looking at the low-level side of the area, whereas silence is dealing with things for the user.

The problem of “too much information” is clearly one that has attracted attention. An awful lot of what LaTeX prints is not interesting, most of the time. I'd say that a better model would be less, more targetted information as standard. A “developer” mode, printing more detail, is still needed but to be honest even then do many people care about some of the stuff that gets logged. Most of the time, I'd say no.

The silence approach (filtering on a per-package basis and also based on specific text in messages) is clearly very powerful but somewhat complicated. I'd hope that the LaTeX3 team will provide some filtering along with properly named messages (rather than the current situation where messages just appear directly in the code). Perhaps not quite as powerful as silence, but a lot better than at the moment.
