---
title: LaTeX2e and e-TeX
layout: post
permalink: /2016/10/31/latex2e-and-e-tex/
categories:
  - General
tags:
  - etex
  - LaTeX2e
---
LaTeX2e was released in 1994 and since then the LaTeX3 Project have been committed to keeping it working smoothly for users. That means balancing up keeping the code stable with fixing bugs and adding new features.

Back in 2003 the team [announced](https://www.latex-project.org/news/latex2e-news/ltnews16.pdf) that the e-TeX extensions would be used by the kernel when they were available. The new primitives offered by e-TeX make many parts of TeX programming easier and  often there's no way in 'classical' TeX to get the same effect. As e-TeX was finalised in 1999, starting to use it seriously in around 2004 meant most people had access to them.

Since then, the availability and use of e-TeX has spread, and almost all users have them available. Indeed, the standard format-building routines for LaTeX have included them for many years. There are also a lot of packages on [CTAN](https://www.ctan.org) that use e-TeX, most obviously any using the [`expl3`](https://ctan.org/pkg/l3kernel) programming language that the LaTeX3 Project have created.

The team had always _meant_ to say at some stage that e-TeX was now required, and indeed thought we had until I checked over the official newsletters! So as of the next LaTeX2e release, scheduled for the start of 2017, the kernel will only build if e-TeX is enabled. For this release, we are likely to add a test for e-TeX but no actual use directly in the kernel, though in the future there will probably be more use of the extensions.
