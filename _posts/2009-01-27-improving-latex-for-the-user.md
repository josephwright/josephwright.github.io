---
title: Improving LaTeX for the user
layout: post
permalink: /2009/01/27/improving-latex-for-the-user/
categories:
  - LaTeX3
  - Packages
  - siunitx
tags:
  - fonts
  - LuaTeX
  - UTF-8
  - XeTeX
---
I've been discussing some points about the future of (La)TeX with various people, and some key issues come to mind. Most LaTeX users do not want to meddle with the internal parts of LaTeX or TeX. In an ideal world, I suspect most users would like to need little beyond the correct document class to get things 'just right' in their layout. Perhaps a few simple settings, but really little more than that.

With the correct packages and class loaded, you can do many things in LaTeX. However, you really shouldn't need to load specific support for hyperlinks, T1 encoding, basic font changing, creating new float types and so on in 2009 (let alone 2010, 2011, _etc_.). The efforts of the [LaTeX3](https://www.latex-project.org/latex3.html) team have to date focussed on programming and to a lesser extent document design. How things will work at the user level is much less clear.

I'd suggest that a real focus on getting something for users would be the best way forward. This might mean less improvement internally, but I'd think that a LaTeX kernel which could do everything in _The LaTeX Companion_ would be pretty successful, even with few changes 'under the hood'. This would mainly be a re-coding excercise from existing packages, which in a way is similar to what I've tried to do with [`siunitx`](https://ctan.org/pkg/siunitx). Much of the basics in `siunitx` are taken from other packages (at least in terms of user interface), but it brings several ideas together in one place. The same idea could easily be applied to the kernel. Of course, this might leave some of the clever ideas for LaTeX3 out of the code at this stage, but I'd hope would get momentum behind a more regularly updated system.

One particular area to think about is fonts. With both XeTeX and LuaTeX able to handle system fonts directly, the basic LaTeX system seems very antiquated. At present, LaTeX3 only requires e-TeX, not LuaTeX (in contrast to [ConTeXt](http://wiki.contextgarden.net) Mark IV). Should the LaTeX team say something like:

> For current testing purposes, only the e-TeX extensions are needed, but this is likely to change. XeTeX or LuaTeX will be required to run the release version of LaTeX3 with full functionality.

I'd say yes, as I think that it's time to move on from complex font installation and usage restrictions. I'd also be very tempted to say that LaTeX3 will assume UTF-8 input unless otherwise specified (as both XeTeX and LuaTeX are native UTF-8 systems).

This type of approach will make LaTeX easier to use, and I'd hope to see it arrive! After all, users are the TeX community.
