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
Bibliographies formatting is complicated, and over the years this has led to the development of a lot of BibTeX styles and tools like <a href="http://ctan.org/pkg/custom-bib">custom-bib</a>. For <a href="http://ctan.org/pkg/biblatex">biblatex</a> users the output style can be altered from within LaTeX, and while there is not yet an equivalent of custom-bib for biblatex there is some <a href="http://tex.stackexchange.com/a/13076/73">excellent advice</a> available for developing new styles.

One of the key ideas of  is to make it possible to address the citation styles in fields where BibTeX could never provide the correct tools. That shows up most obviously in humanities, where the position of citations in the output needs to feed back into how they appear. Life gets even more complicated when you consider areas that need specialised fields included in their bibliographies: a classic example is law. There are already developments under-way to help support these situation, for example <a href="http://biblatex-biber.sourceforge.net/">Biber</a>-based flexible data model. Addressing the needs of style authors properly requires co-ordination between the <a title="biblatex: A team to continue the work" href="http://www.texdev.net/2012/04/23/biblatex-a-team-to-continue-the-work/">core biblatex team</a> and the style creators, and between different style authors. The question of how to achieve this communication <a href="http://tex.stackexchange.com/q/55235/73">came up recently on TeX-sx</a>.

There are at least a couple of obvious ways for people to stay in touch with each other. First, where there is a need for a specific function to be added to biblatex, the <a href="https://github.com/plk/biblatex/">package GitHub site</a> is the place to go. Adding issues makes sure that they don't get lost in direct e-mails, and also ensures that anyone with a point of view can comment. Secondly, for more open discuss TUG have a <a href="http://tug.org/mailman/listinfo/biblio">bibliography mailing list</a>. To date, this has not been very heavy in terms of traffic, but it would be an ideal forum to co-ordinate effort. It's publicly archived and anyone can join, so there is no danger of loosing important comments.

Of course, there are other ways to communicate too! All of the team are active on <a href="http://tex.stackexchange.com">TeX-sx</a>, and when we can we pick up biblatex issues and add them to the to do list. Direct e-mail works too, and I'm sure some style authors will go for direct communication. The key thing is to use the power of biblatex to make life easier for the end-user.