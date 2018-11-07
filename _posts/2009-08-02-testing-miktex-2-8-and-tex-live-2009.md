---
title: Testing MiKTeX 2.8 and TeX Live 2009
layout: post
permalink: /2009/08/02/testing-miktex-2-8-and-tex-live-2009/
categories:
  - TeXworks
tags:
  - MiKTeX
  - TeX Live
  - XeTeX
---
Both [MiKTeX](https://www.miktex.org/) and [TeX Live](https://tug.org/texlive/) have new versions in the offing.  I've been testing out both MiKTeX 2.8 and TeX Live 2009, to keep up to date with what is happening. In the past, I've tended to stick with MiKTeX as it is designed for Windows, and so can make some platform-specific decisions and be more focussed. However, the TeX Live team have done a lot of work to make TeX Live usable across platforms, and there are advantages to that approach.

Looking through the feature lists, a lot of the new features are common to the two systems, for example:

- [TeXworks](https://tug.org/texworks) installed as a distribution-maintained editor.
- [XeTeX](https://tug.org/xetex/) version 0.9995 (which includes the new primitives that the [LaTeX3](https://www.latex-project.org/latex3.html) team asked for).
- Some `\write18` functions enabled without turning on full `\write18` support: this is used to allow 'safe' functions.

There are, of course, also differences. For example, only TeX Live includes [LuaTeX](http://www.luatex.org) at present. I also notice that MiKTeX 2.8 is adding the full path of files to the log, whereas in the past you got the relative path. I'm not so sure this is a good idea: it makes things rather wordy, and also the log will vary between systems: not so great. On the other hand, MiKTeX 2.8 does provide user-specific texmf directories. For multi-user systems, this is a real bonus: you can use the auto-install system without needing to be the Administrator.

As I said, I've tended to use MiKTeX to date as it's been the best 'fit' on Windows. The latest version of TeX Live makes this a pretty tight call, I think. If you are happy installing a full TeX system (which I do), then there is very little in it. MiKTeX still has the edge for small installations, as the auto-install system really pays off there.
