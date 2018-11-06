---
id: 1376
title: Co-ordinating biblatex style development
date: 2012-05-16T08:19:52+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1376
permalink: /2012/05/16/co-ordinating-biblatex-style-development/
categories:
  - biblatex
  - Packages
---
Bibliographies formatting is complicated, and over the years this has led to the development of a lot of BibTeX styles and tools like [custom-bib](http://ctan.org/pkg/custom-bib). For [biblatex](http://ctan.org/pkg/biblatex) users the output style can be altered from within LaTeX, and while there is not yet an equivalent of custom-bib for biblatex there is some [excellent advice](http://tex.stackexchange.com/a/13076/73) available for developing new styles.

One of the key ideas of  is to make it possible to address the citation styles in fields where BibTeX could never provide the correct tools. That shows up most obviously in humanities, where the position of citations in the output needs to feed back into how they appear. Life gets even more complicated when you consider areas that need specialised fields included in their bibliographies: a classic example is law. There are already developments under-way to help support these situation, for example [Biber](http://biblatex-biber.sourceforge.net/)-based flexible data model. Addressing the needs of style authors properly requires co-ordination between the [core biblatex team](http://www.texdev.net/2012/04/23/biblatex-a-team-to-continue-the-work/) and the style creators, and between different style authors. The question of how to achieve this communication [came up recently on TeX-sx](http://tex.stackexchange.com/q/55235/73).

There are at least a couple of obvious ways for people to stay in touch with each other. First, where there is a need for a specific function to be added to biblatex, the [package GitHub site](https://github.com/plk/biblatex/) is the place to go. Adding issues makes sure that they don't get lost in direct e-mails, and also ensures that anyone with a point of view can comment. Secondly, for more open discuss TUG have a [bibliography mailing list](http://tug.org/mailman/listinfo/biblio). To date, this has not been very heavy in terms of traffic, but it would be an ideal forum to co-ordinate effort. It's publicly archived and anyone can join, so there is no danger of loosing important comments.

Of course, there are other ways to communicate too! All of the team are active on [TeX-sx](http://tex.stackexchange.com), and when we can we pick up biblatex issues and add them to the to do list. Direct e-mail works too, and I'm sure some style authors will go for direct communication. The key thing is to use the power of biblatex to make life easier for the end-user.
