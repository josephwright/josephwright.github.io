---
id: 425
title: notes2bib two
date: 2009-09-28T13:29:18+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=425
permalink: /2009/09/28/notes2bib-two/
categories:
  - LaTeX3
  - Packages
tags:
  - notes2bib
---
I've just send a new version of my <a title="Integrating notes into the bibliography" href="http://ctan.org/pkg/notes2bib">notes2bib</a> package to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a>. notes2bib lets you include the text of notes in the body of a file, but have them appear in the bibliography: for chemists, this is pretty common. The new version is a re-working of the existing code plus some ideas I explored with an experimental version called xnotes2bib. I've re-jigged the options to make them more descriptive, and some of the macros have been renamed. My original choices were not always the best. The biggest change, though, is internally, where I've recoded everything using <a title="The expl3 bundle: Low-level LaTeX3 programming conventions" href="http://ctan.org/pkg/l3kernel">expl3</a>, the coding base for LaTeX3. That means that users will need to install a couple of support packages, but I hope means that the code should make a bit more sense (at least to me!). The only way expl3 will get tested is if people use is, so I'm prepared to have a go and hope everything works. So far, all looks good.
