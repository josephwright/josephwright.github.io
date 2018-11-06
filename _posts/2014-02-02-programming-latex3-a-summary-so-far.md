---
id: 1681
title: 'Programming LaTeX3: A summary so far'
date: 2014-02-02T10:48:47+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1681
permalink: /2014/02/02/programming-latex3-a-summary-so-far/
categories:
  - LaTeX3
tags:
  - expl3
---
Use of the [LaTeX3 programming layer 'expl3'](http://www.latex-project.org/latex3.html) in LaTeX2e packages is continuing to grow. Ideally, the team would have a nice easy-to-follow _Programming LaTeX3_ book to support this, but as the language is still developing and because writing such a guide is _hard_ we are not in that position just at the moment. At the moment, the nearest we get is a [series of posts](http://www.texdev.net/tag/programming-latex3/) I wrote here a little while ago now, trying to at least put some basics down. What I'd like to build up is a 'self-contained' story, based on the idea that the reader knows how to use LaTeX as an 'end user' (making documents), but with no particular assumptions about programming. I'm hoping to look again at some of these topics in the coming months, but for the moment it seems like a good idea to summarise what we have so far.

To date, the series covers:

- [A general introduction](http://www.texdev.net/2011/12/06/programming-latex3-introduction/) and [background](http://www.texdev.net/2011/12/07/programming-latex3-background/) (these two probably work together as one 'lesson')
- [The programming environment](http://www.texdev.net/2011/12/11/programming-latex3-the-programming-environment/)
- [Creating 'functions'](http://www.texdev.net/2011/12/14/programming-latex3-creating-functions/)
- [The idea of category codes and token lists](http://www.texdev.net/2011/12/21/programming-latex3-category-codes-tokens-and-token-lists/)
- [Storing tokens in variables](http://www.texdev.net/2011/12/26/programming-latex3-token-list-variables/)
- [More on token list variables](http://www.texdev.net/2012/01/22/programming-latex3-more-on-token-list-variables/)
- [Integers and integer variables](http://www.texdev.net/2012/02/07/programming-latex3-integers-and-integer-expressions/)
- [Expandablity](http://www.texdev.net/2012/04/21/programming-latex3-expandability/)
- [Controlling expansion](http://www.texdev.net/2012/04/29/programming-latex3-more-on-expansion/)

The posts run basically in order, so if you are looking to learn then start with the first one and work your way down.

Of course, looking back I think some revision would be handy: for example, now we have an FPU it might be useful to cover that around the same point as integers. I guess what might be sensible is to look seriously at putting together something more structured which can be revised: perhaps it is time for that book!
