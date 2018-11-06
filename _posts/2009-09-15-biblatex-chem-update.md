---
id: 409
title: biblatex-chem update
date: 2009-09-15T14:45:22+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=409
permalink: /2009/09/15/biblatex-chem-update/
categories:
  - biblatex
  - Packages
tags:
  - biblatex-chem
---
I've just spotted a bug in [biblatex-chem](http://ctan.org/pkg/biblatex-chem), and a fix is on the way to [CTAN](http://www.ctan.org). It looks like changes in the [biblatex ](http://ctan.org/pkg/biblatex)core have made the comma after journal titles when using the chem-rsc style disappear. This was working earlier: I've retested an old version and it is not due to anything I've done.

On another matter, I've been asked to look at turning page ranges into single pages in biblatex-chem. I need to add the appropriate functions to biblatex, so there may be a delay (I have lots on at the moment). It is definitely on my list to do. Why do this? Well, some journals insist on first-page only, but in a database both pages will be present. So the code needs to handle things. There should be another update once I sort this: a few days.
