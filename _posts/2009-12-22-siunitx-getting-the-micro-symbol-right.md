---
id: 589
title: 'siunitx: Getting the micro symbol right'
date: 2009-12-22T21:12:47+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=589
permalink: /2009/12/22/siunitx-getting-the-micro-symbol-right/
categories:
  - Packages
  - siunitx
tags:
  - micro
  - XeTeX
---
I get a few e-mails about [siunitx](https://ctan.org/pkg/siunitx) and the micro symbol. People tend to be surprised that the symbol ‘sticks’ to a look very much like Computer Modern. The reason is that picking a proper upright (not italic) μ is not so easy in TeX. You don't get one in Computer Modern, so siunitx takes one from the TS1 (text support) set in the absence of a better plan. I've set up some auto-detection for a few obvious alternatives (such as the [upgreek](https://ctan.org/pkg/upgreek) package), but that doesn't really work for [XeTeX](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=XeTeX) users.

XeTeX users are likely to load system fonts, and I'd hope be using UTF-8 input. That makes it hard to auto-detect what they are doing, but should make life easier for them to get things right. A lot of more comprehensive fonts include Greek letters in the main font, so getting the μ right is simple:

```latex
\sisetup{
  mathsmu = \text{μ},
  textmu  = μ
}
```

or for people testing [version 2 of siunitx](http://developer.berlios.de/projects/siunitx/):

```latex
\sisetup{
  maths-micro = \text{μ},
  text-micro  = μ
}
```

There may be a bit of testing required: this will not work if, for example, you are using the Latin Modern font.
