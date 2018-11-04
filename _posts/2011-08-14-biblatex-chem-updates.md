---
id: 1079
title: biblatex-chem updates
date: 2011-08-14T09:59:34+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1079
permalink: /2011/08/14/biblatex-chem-updates/
categories:
  - biblatex
  - Packages
tags:
  - biblatex-chem
---
Recent changes to <a title="Programmable Bibliographies and Citations" href="http://ctan.org/pkg/biblatex">biblatex</a> (in v1.6) mean that the <a title="A set of biblatex implementations of chemistry-related bibliography styles" href="http://ctan.org/pkg/biblatex-chem">biblatex-chem</a> bundle is currently broken. I've not released a quick-fix as there are some long-standing issues to address in biblatex-chem. When I initially wrote the code, I started from scratch and defined only what I wanted. That works, but means that any changes in biblatex are not automatically picked up. From <a title="A biblatex implementation of the IEEE bibliography style" href="http://ctan.org/pkg/biblatex-ieee">biblatex-ieee</a>, I took the alternative approach and worked from the standard biblatex styles to what was needed. That's a better long-term approach, so it's the one I'm now bringing to biblatex-chem. It will take a little while, so user might want to keep an eye on the <a href="https://github.com/josephwright/biblatex-chem">development code</a>.