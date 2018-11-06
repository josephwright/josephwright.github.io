---
title: Babel woes
layout: post
permalink: /2009/02/01/babel-woes/
categories:
  - Packages
  - siunitx
tags:
  - babel
  - UTF-8
---
I've had a couple of [`babel`](https://ctan.org/pkg/babel)-related bug reports for [`siunitx`](https://ctan.org/pkg/siunitx).  The first was with the Spanish language option, where the `\percent` unit misbehaves as `\%` is redefined by babel. My fix for this has then caused a problem with the Italian language option, as it makes " an active character. So the latest release (v1.2d) fixes this too: apologies for the problems.

All of this makes more more eager than ever that a general move to UTF-8 input happens. This should cut down on the need for babel. At the same time, an updated LaTeX kernel ([LaTeX3](https://www.latex-project.org/latex3.html)) which includes more functionality would also help package authors know what to expect.
