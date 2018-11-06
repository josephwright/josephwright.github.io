---
title: Storing lists of tokens
layout: post
permalink: /2008/12/18/storing-lists-of-tokens/
categories:
  - LaTeX3
---
[LaTeX3](https://www.latex-project.org/latex3.html) separates out macros which do something (functions) from those used to store information. As has been pointed out to me, the later are lists of _tokens_ not characters. TeX already provides us with toks (token registers), and so LaTeX3 calls macros that store token lists “token list pointers”. There's been some discussion recently about this name, and [Will Robertson](http://www.mecheng.adelaide.edu.au/~will/) has suggested just “token lists” would be better. I quite like the idea (pointers makes it sound like some low-level memory thing), but I'm not sure if the team will go for it.
