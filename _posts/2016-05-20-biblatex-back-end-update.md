---
id: 1881
title: Biblatex back-end update
date: 2016-05-20T19:47:29+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1881
permalink: /2016/05/20/biblatex-back-end-update/
categories:
  - biblatex
  - Packages
---
I wrote recently abut the need to [manage `biblatex` back-ends](https://www.texdev.net/2016/03/13/managing-biblatex-backends/), and thoughts the maintenance team had on which way to proceed.

After a bit of thought, we've gone for a solution we hope works for users and for us. Reversing what seemed like a 'good idea at the time', we've re-integrated (almost) all of the TeX code into one pathway. This is focussed on Biber, but we have a small stub that converts the relevant parts to work with BibTeX. So users how don't need Biber or can't use it can still use BibTeX and get mainly the same results.

There are a few changes, mainly related to places where BibTeX and Biber had ended up with different interfaces and where BibTeX can't (reasonably) support the Biber one. In those places we've dropped the ability to use a 'BibTeX alternative pathway' as it makes the code complex and makes switching between back-ends tricky.

Hopefully the balance we've gone for will work for everyone: you can still use BibTeX, it still does almost everything it always has with `biblatex`, but we've got a more sustainable code base for the future.
