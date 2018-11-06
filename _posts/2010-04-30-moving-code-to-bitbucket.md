---
id: 685
title: Moving code to BitBucket
date: 2010-04-30T09:24:43+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=685
permalink: /2010/04/30/moving-code-to-bitbucket/
categories:
  - General
tags:
  - BitBucket
  - Git
  - Mercurial
  - Version control
---
As the number of packages I've written has grown keeping a track of everything has got more complex for me. Not having a background in programming, I've very much had to learn things ‘on the job’. One thing I've been doing for a while now is using a version control system for the new version of [`siunitx`](https://ctan.org/pkg/siunitx) and working as part of the [LaTeX3 Project](https://www.latex-project.org/latex3.html). The LaTeX3 Project uses the [Subversion](http://subversion.apache.org/) system (also known as ‘SVN’), and so I've been using the same system for siunitx version 2 (hosted by [BerliOS](http://www.berlios.de/)). I've now decided to get a bit more systematic, using the service provided by [BitBucket](https://bitbucket.org/).

## Aims

There are a few different things that I wanted to get sorted out with all of my packages. First, I think it is useful to make the code (and code changes) publicly available in one place. That is what version control systems provide: you get a list of changes, with hopefully some notes on what was going on.  That also makes it possible for other people to easily suggest patches (if they want to, of course!). Second, tracking bugs and feature requests really requires some kind of structure. I currently have a long list of e-mails that list things to think about: making these both publicly available and organised is a good idea. That helps me, and also lets user see what has already been logged. Third, it is useful if there is a way of having on-line documentation, for example using a wiki.

## Moving to BitBucket

I had a look at various approaches to doing all of that. I've had a few issues with [BerliOS](http://www.berlios.de/), and as I've used it I've realised that the interface is rather awkward. Two services which look rather more helpful are [BitBucket](https://bitbucket.org/) and [GitHub](https://github.com/). Both of these are based around distributed version control systems: [Mercurial](http://mercurial.selenic.com/) and [Git](http://git-scm.com/), respectively. I'm not going to go into the details of either of these (or the differences between them), but Mercurial seemed a bit easier to use to me so I decided to go that way. BitBucket includes all of the bug tracking and wiki features on my list of ideas, and so far I've found the interface clear and powerful.

Over the last couple of days I've uploaded basically all of the current versions of [my packages to BitBucket](https://bitbucket.org/josephwright/). As most of these were written without formal version control, I've had to ‘reconstruct’ the historical changes from my archive. I've aimed for a balance between providing information and my time: the history goes back to the first version of the current releases (for example, from v3.0 for [`achemso`](https://ctan.org/pkg/achemso), which is currently on v3.4f). Of course, any new versions will appear on BitBucket. I'm now working on moving all of the issues into the bug databases. I'll also look at the wiki side of things: I'll try to put some basic installation and use information, and perhaps some frequently asked questions. BitBucket includes RSS feeds, so anyone interested can follow what is going on.

## The beamer connection

I should add that one of the reasons for looking at all of this was the recent news that the [`beamer`](https://ctan.org/pkg/beamer) package has a [new maintainer](http://permalink.gmane.org/gmane.comp.tex.latex.beamer.general/2286). I've taken a bit of interest in this, and as the [code](https://bitbucket.org/rivanvx/beamer/wiki/Home) has been moved to BitBucket, took a look at the facilities on offer there. As a result, I've been given access to the new repository. I have a few vague ideas about areas to look at, but at the moment nothing definite!

## Get involved

Anyone interested is of course free to contribute. Adding any bugs,  enhancements or ideas to the databases is one of the easiest way to do  that. If anyone wants access to edit the wikis or add code, [drop me a line](mailto:joseph.wright@morningstar2.co.uk).
