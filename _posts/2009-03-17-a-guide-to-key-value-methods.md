---
title: A guide to key-value methods
layout: post
permalink: /2009/03/17/a-guide-to-key-value-methods/
categories:
  - General
tags:
  - key-value input
  - keyval
  - kvoptions
  - pgfkeys
  - xkeyval
---
I have a second draft for [TUGBoat](https://tug.org/tugboat/) on the go at the moment: an [article on implementing key-value input](/wp-content/uploads/2009/03/keyval.pdf). These are widely used in LaTeX packages, but are also usful in plain TeX. As well as the original [`keyval`](https://ctan.org/pkg/keyval) package, we have [`xkeyval`](https://ctan.org/pkg/xkeyval), [`kvoptions`](https://ctan.org/pkg/kvoptions) and [`kvsetkeys`](https://ctan.org/pkg/kvsetkeys) for managing key–value input. However, actually getting started with these as a LaTeX programmer can be somewhat difficult. The aim of the article is to lower the barrier to getting going with key-value methods. As well as the keyval-based information, the pgfkeys package (part of the [`pgf`](https://ctan.org/pkg/pgf) bundle) is also covered (thanks to Christian Feuersänger).
