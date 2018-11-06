---
id: 45
title: Advanced features of xkeyval for LaTeX3
date: 2008-12-24T18:13:39+00:00
author: josephwright
layout: post
guid: http://texdev.wordpress.com/?p=45
permalink: /2008/12/24/advanced-features-of-xkeyval-for-latex3/
categories:
  - LaTeX3
---
Currently, [LaTeX3](http://www.latex-project.org/latex3.html) only provides parsing of key–value input into separated keys and values. I've written the keys3 package as a possible implementation of keyval for LaTeX3: this is based on pgfkeys from the [`pgf`](https://ctan.org/pkg/pgf) system. However, there are some features of the [`xkeyval`](https://ctan.org/pkg/xkeyval) package that I've not yet covered. In particular, I'm wondering about the “preset” keys system (`\presetkeys` and relatives) and the “pointer” system (`\savekeys` and so on). I've not really used these, so I'm not sure what might be needed for LaTeX3.

I think that LaTeX3 needs to have built-in keyval support which can cover everything that can be done by add-ons in LaTeX2e. I'd appreciate ideas on what needs to be added to keys3 to achieve this.
