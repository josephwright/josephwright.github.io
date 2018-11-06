---
id: 25
title: Storing lists of tokens
date: 2008-12-18T08:12:07+00:00
author: josephwright
layout: post
guid: http://texdev.wordpress.com/?p=25
permalink: /2008/12/18/storing-lists-of-tokens/
categories:
  - LaTeX3
---
<a href="http://www.latex-project.org/latex3.html">LaTeX3</a> separates out macros which do something (functions) from those used to store information. As has been pointed out to me, the later are lists of <em>tokens</em> not characters. TeX already provides us with toks (token registers), and so LaTeX3 calls macros that store token lists “token list pointers”. There's been some discussion recently about this name, and <a href="http://www.mecheng.adelaide.edu.au/~will/">Will Robertson</a> has suggested just “token lists” would be better. I quite like the idea (pointers makes it sound like some low-level memory thing), but I'm not sure if the team will go for it.
