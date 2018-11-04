---
id: 657
title: XeTeX, chemstyle and chemscheme
date: 2010-03-29T20:15:08+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=657
permalink: /2010/03/29/xetex-chemstyle-and-chemscheme/
categories:
  - Packages
tags:
  - chemscheme
  - chemstyle
  - psfrag
  - XeTeX
---
There have been a few queries recently about using my <a title="Styles and schemes for chemistry" href="http://ctan.org/pkg/chemstyle">chemstyle</a> package with <a title="XeTeX" href="http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=xetex">XeTeX</a>. The problems arise when people attempt to use the <code>\schemeref</code> macro, which is defined by the ‘low-level’ <a title="Styles and schemes for chemistry" href="http://ctan.org/pkg/chemstyle">chemscheme</a> package, which is loaded by chemstyle. For those of you not familiar with the package, it's for chemistry graphics (which are usually called ‘schemes’), and is for putting in reference numbers automatically.

The problems arise because chemstyle ultimately relies on <a title="Replace strings in encapsulated PostScript figures" href="http://ctan.org/pkg/psfrag">psfrag</a> for the graphic manipulations. To the best of my knowledge, psfrag can't be made to work with XeTeX, which means that neither can my <code>\schemeref</code> macro. I've just uploaded a version of chemstyle to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a> which says this, and issues a warning if used with XeTeX. I do hope that helps a little.