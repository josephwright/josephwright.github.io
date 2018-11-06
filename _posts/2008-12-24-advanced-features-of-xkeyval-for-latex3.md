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
Currently, <a href="http://www.latex-project.org/latex3.html">LaTeX3</a> only provides parsing of key–value input into separated keys and values. I've written the keys3 package as a possible implementation of keyval for LaTeX3: this is based on pgfkeys from the <a href="http://ctan.org/pkg/pgf">pgf</a> system. However, there are some features of the <a href="http://ctan.org/pkg/xkeyval">xkeyval</a> package that I've not yet covered. In particular, I'm wondering about the “preset” keys system (<code>\presetkeys</code> and relatives) and the “pointer” system (<code>\savekeys</code> and so on). I've not really used these, so I'm not sure what might be needed for LaTeX3.

I think that LaTeX3 needs to have built-in keyval support which can cover everything that can be done by add-ons in LaTeX2e. I'd appreciate ideas on what needs to be added to keys3 to achieve this.
