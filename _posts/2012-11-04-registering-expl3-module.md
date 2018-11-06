---
id: 1566
title: Registering expl3 module
date: 2012-11-04T18:32:57+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1566
permalink: /2012/11/04/registering-expl3-module/
categories:
  - LaTeX3
---
Namespace management in TeX is a co-operative affair: we all share one space, so conventions such as <code>\my@clever@macro</code> are important. For LaTeX2e work, this has always been done on a very informal basis: look around and find a space! For LaTeX3, it seems like a good idea to make things a little bit more ordered. We've therefore set up a simple <a href="https://github.com/latex3/svn-mirror/blob/master/l3kernel/l3prefixes.csv">flat-file prefix register</a>, which will track all of the prefixes in use in expl3 code (provided people <a href="mailto:modules@latex-project.org">tell us</a>, of course).
