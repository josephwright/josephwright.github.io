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
Recent changes to [`biblatex`](https://ctan.org/pkg/biblatex) (in v1.6) mean that the [`biblatex-chem`](https://ctan.org/pkg/biblatex-chem) bundle is currently broken. I've not released a quick-fix as there are some long-standing issues to address in biblatex-chem. When I initially wrote the code, I started from scratch and defined only what I wanted. That works, but means that any changes in biblatex are not automatically picked up. From [`biblatex-ieee`](https://ctan.org/pkg/biblatex-ieee), I took the alternative approach and worked from the standard biblatex styles to what was needed. That's a better long-term approach, so it's the one I'm now bringing to biblatex-chem. It will take a little while, so user might want to keep an eye on the [development code](https://github.com/josephwright/biblatex-chem).
