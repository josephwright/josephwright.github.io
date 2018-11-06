---
id: 236
title: A guide to key-value methods
date: 2009-03-17T20:30:45+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=236
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
I have a second draft for <a title="The Communications of the TeX Users Group" href="http://www.tug.org/tugboat/">TUGBoat</a> on the go at the moment: an <a href="http://www.texdev.net/wp-content/uploads/2009/03/keyval.pdf">article on implementing key-value input</a>. These are widely used in LaTeX packages, but are also usful in plain TeX. As well as the original <a title="Process 'key=value' schemes" href="http://www.ctan.org/pkg/keyval">keyval</a> package, we have <a title="Extension of the keyval package" href="http://www.ctan.org/pkg/xkeyval">xkeyval</a>, <a title="Key value format for package options" href="http://www.ctan.org/pkg/kvoptions">kvoptions</a> and <a title="Key value parser with default handler support" href="http://www.ctan.org/pkg/kvsetkeys">kvsetkeys</a> for managing key–value input. However, actually getting started with these as a LaTeX programmer can be somewhat difficult. The aim of the article is to lower the barrier to getting going with key-value methods. As well as the keyval-based information, the pgfkeys package (part of the <a title="Create PostScript and PDF graphics in TeX" href="http://www.ctan.org/pkg/pgf">pgf</a> bundle) is also covered (thanks to Christian Feuersänger).
