---
id: 1570
title: Keeping releases in sync
date: 2012-11-25T10:15:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1570
permalink: /2012/11/25/keeping-releases-in-sync/
categories:
  - General
---
As a package developer, I regularly send material to [CTAN](https://www.ctan.org). Once my code gets uploaded, there is not much I can do about it spreading around the world. There's always a slight delay in the various CTAN mirrors picking up new material, while the code only changes [TeX Live](http://tug.org/texlive) and [MiKTeX](http://www.miktex.org) once the maintainers of those systems spot the CTAN changes.

For a single package upload, that process simply means a little bit of a delay between me saying that something is fixed and everyone being able to use it. However, where there are linked changes in more than one package then life gets a bit more complicated. A classic situation is [`siunitx`](https://ctan.org/pkg/siunitx), which uses the [LaTeX3 programming environment](https://ctan.org/pkg/l3kernel). I do the releases for LaTeX3 so if there is an issue which needs a change in both `siunitx` and the LaTeX3 code both get updated on CTAN at the same time. However, it's not unknown for TeX Live or MiKTeX to pick up only one change initially, leading to issues for end users. That's a pain, but there is little I can do about it as I don't control that process.
