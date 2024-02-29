---
title: Registering expl3 module
layout: post
permalink: /2012/11/04/registering-expl3-module/
categories:
  - expl3
---
Namespace management in TeX is a co-operative affair: we all share one space,
so conventions such as `\my@clever@macro` are important. For LaTeX2e work, this
has always been done on a very informal basis: look around and find a space!
For LaTeX3, it seems like a good idea to make things a little bit more ordered.
We've therefore set up a simple [flat-file prefix
register](https://github.com/latex3/latex3/blob/main/l3kernel/doc/l3prefixes.csv),
which will track all of the prefixes in use in expl3 code (provided people
[tell us](mailto:modules@latex-project.org), of course).
