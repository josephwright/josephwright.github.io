---
title: Sorting beamer bugs
layout: post
permalink: /2011/09/11/sorting-beamer-bugs/
categories:
  - beamer
---
The [`beamer`](https://ctan.org/pkg/beamer) class is rightly regarded as the leading way to produce presentations with LaTeX. A while ago now, there was a need to find a new maintainer, and [Vedran Miletić](https://bitbucket.org/rivanvx) volunteered to take over. At the same time, I'd said I would be willing to at least take on some formal connection, if only to get available patches integrated into the code.

Vedran has fixed a number of bugs in `beamer`, but the [list has been building up](https://bitbucket.org/rivanvx/beamer/issues?status=new&status=open). I've spoken with Vedran about this, and as I suspected he's rather busy! There's also the fact that `beamer` works for most people most of the time. So for the moment I'm going to be dealing with keeping on top of the bug list.

As a first stage, I'm going through the list, removing anything that is not really a `beamer` issue (such as passing issues with `hyperref`) or which I can't reproduce. I'm also picking up on bugs where there is a patch available: those can go into the code pretty much straight away. The next phase will be to sort bugs that seem to have some obvious fix. This is not so easy as `beamer` is rather complex internally, and I want to avoid breaking anything.

I'd expect to update [CTAN](https://www.ctan.org) once I've had a look through all of the bugs. Probably by the end of this week this first phase should be done, so I'd expect there to be a run of new `beamer` versions over the coming weeks.

I can't promise to sort out all of the bugs, but I'd like to at least try to get the list down. If anyone wants to help out (or indeed to take over!) then they are, as usual, welcome to [make contact.](mailto:joseph@texdev.net)
