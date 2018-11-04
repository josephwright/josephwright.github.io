---
id: 1107
title: Sorting beamer bugs
date: 2011-09-11T11:31:17+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1107
permalink: /2011/09/11/sorting-beamer-bugs/
categories:
  - beamer
---
The <a title="A LaTeX class for producing presentations and slides" href="http://ctan.org/pkg/beamer">beamer</a> class is rightly regarded as the leading way to produce presentations with LaTeX. A while ago now, there was a need to find a new maintainer, and <a href="https://bitbucket.org/rivanvx">Vedran Miletić</a><a href="http://permalink.gmane.org/gmane.comp.tex.latex.beamer.general/2286"> volunteered to take over</a>. At the same time, I'd said I would be willing to at least take on some formal connection, if only to get available patches integrated into the code.

Vedran has fixed a number of bugs in beamer, but the <a href="https://bitbucket.org/rivanvx/beamer/issues?status=new&amp;status=open">list has been building up</a>. I've spoken with Vedran about this, and as I suspected he's rather busy! There's also the fact that beamer works for most people most of the time. So for the moment I'm going to be dealing with keeping on top of the bug list.

As a first stage, I'm going through the list, removing anything that is not really a beamer issue (such as passing issues with hyperref) or which I can't reproduce. I'm also picking up on bugs where there is a patch available: those can go into the code pretty much straight away. The next phase will be to sort bugs that seem to have some obvious fix. This is not so easy as beamer is rather complex internally, and I want to avoid breaking anything.

I'd expect to update <a title="LaTeX3: More use, more work" href="http://www.ctan.org">CTAN</a> once I've had a look through all of the bugs. Probably by the end of this week this first phase should be done, so I'd expect there to be a run of new beamer versions over the coming weeks.

I can't promise to sort out all of the bugs, but I'd like to at least try to get the list down. If anyone wants to help out (or indeed to take over!) then they are, as usual, welcome to <a href="mailto:joseph.wright@morningstar2.co.uk">make contact.</a>