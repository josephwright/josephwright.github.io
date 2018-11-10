---
title: beamer developments
layout: post
permalink: /2017/12/17/beamer-developments/
categories:
  - beamer
  - Packages
tags:
  - beamer
  - github
  - l3build
  - testing
---
I've been looking after `beamer` for a few years, largely 'by accident' (this seems to happen quite a lot). Relatively recently, I [moved the code](/2016/11/27/beamer-moves-to-github//2016/11/27/beamer-moves-to-github/) from [BitBucket](https://bitbucket.org) to [GitHub](https://github.com), largely because there's a slow drift there for LaTeX projects. The advantage of that is the chance to pick up additional help.

Eagle-eyed readers will have noticed that over the last few months there have been a lot of `beamer` check-ins from [Louis Stuart](https://github.com/louisstuart96). He's doing excellent work on tackling a lot of tricky `beamer` bugs, and I hope this will mean a better user experience. Of course, changing a complex product like `beamer` does have some risks, and so it's also important to get the release set up working smoothly. To that end, I've migrated from some custom `Makefile` structures to using [`l3build`](https://ctan.org/pkg/l3build) (with some new features in the latter to help). That should mean a more regular release schedule.  It also means we can integrate testing into the coding: currently there is just the one test, but I'd welcome additions!
