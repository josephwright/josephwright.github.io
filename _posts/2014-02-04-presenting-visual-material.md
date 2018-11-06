---
id: 1686
title: Presenting visual material
date: 2014-02-04T08:49:20+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1686
permalink: /2014/02/04/presenting-visual-material/
categories:
  - General
tags:
  - posters
  - presentations
---
I've recently been thinking about how best to present 'visual' material: presentations, lectures and academic posters. As a 'LaTeX regular' I tend to do that in LaTeX (using [`beamer`](https://ctan.org/pkg/beamer)), but in many ways what I've been thinking about is entirely independent of the tool I use. Looking around the TeX world, I found a couple of very interesting articles in the [PracTeX journal](http://tug.org/pracjourn/archive.html), [one on posters](http://tug.org/pracjourn/2010-2/rogerio.html) and [one on presentations](http://tug.org/pracjourn/2010-2/hofert.html). As you might expect, they contain some 'technical' advice but are worth a read whatever tool you use to make your visual material. (Many people who use LaTeX for articles prefer more visual tools for posters in particular.)

## Presentations

The core idea in the paper on [presentations](http://tug.org/pracjourn/2010-2/hofert.html) is I guess 'rolling your own' in terms of producing your slides. On the the authors is Marcus Kohm, so it's no surprise that there is a strong focus on using [KOMA-Script](http://www.komascript.de/) as a general-purpose class, and making design changes to suit the screen rather than print. There are a couple of reasons suggested for doing this. The first is that, like any 'pre-build' approach, it's easy to just use the defaults of say [`beamer`](https://ctan.org/pkg/beamer) or [`powerdot`](https://ctan.org/pkg/powerdot) and make a presentation that is very similar to lots of other ones. If you do the design yourself as a 'one off' that's much less likely to be a concern. The other argument was that in some ways dedicated presentation classes make it too easy to use lots of 'effects' (such as the `beamer` overlay concept I [looked at recently](/2014/01/17/the-beamer-slide-overlay-concept/)).

I'm not sure I'd want to make my own slides from scratch every time I make a presentation: there are reasons that there are dedicated classes. However, I'd say the points about design and 'effects' are both valid. I increasingly use pretty 'basic' slides, which don't have much in the way of 'fancy' design or dynamic content, and find that these work just as well if not better than more complex ones. Overlays and similar do have a use, and I do use them when they make good sense, but that's actually pretty rare.

## Posters

The message in the [article on posters](http://tug.org/pracjourn/2010-2/rogerio.html) is in some ways the same as the presentation one: the standard designs don't work that well. Academic posters tend to be very text-heavy, and a multi-column design with a few small graphics is one you see repeated a lot. The article suggests a radically-different approach: essentially no words and just graphical elements. That's not necessarily LaTeX's strength, but the authors do a goo d job using TikZ to showcase their argument.

I've never quite had the nerve to make a poster with essentially no text.  However, I do see the point that mainly graphical posters in many ways work better than putting your entire paper on the wall. There's always that worry that once a poster goes up, you can't be sure you'll be there to talk to anyone interested and so a few words are in some ways a 'safety net'.

## Conclusion

Both articles give you something to think about. Even if you do all of your slides and posters in visual tools (PowerPoint, KeyNote, Illustrator, _etc._), the core messages are still valid. I'd say we can all learn a little here: worth a read!
