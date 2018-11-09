---
title: Moving siunitx to LaTeX3 coding
layout: post
permalink: /2009/07/18/moving-siunitx-to-latex3-coding/
categories:
  - LaTeX3
  - Packages
  - siunitx
---
If you take a look at the [development version](https://github.com/josephwright/siunitx) of [`siunitx`](https://ctan.org/pkg/siunitx), you will find that I'm getting on with moving the code over to using [LaTeX3](https://www.latex-project.org/latex3.html) coding internally. That does not mean that the package will not work using LaTeX2e: everything still works nicely in a normal LaTeX document! However, it does mean that I can use the new coding ideas to make my life easier, and hopefully the code more robust and a little faster.

I've also moved to using my own LaTeX3 keyval package for option handling. I recently added it to the main LaTeX3 code base, so I know that it will be available if LaTeX3 is! Following the pattern for other LaTeX3 keyval settings, I'm changing the original key naming plan somewhat. I'll probably post more detail on this once things are working a little better. The idea is to use more descriptive key names that then current version of `siunitx`, for example:

```latex
\sisetup{
  group-digits         = true,
  round-mode           = places,
  round-places         = 3,
  separate-uncertainty = true
}
```

There will be a delay of a week as I'm on holiday, then I hope to get the experimental code doing almost everything that the current release version does. There is going to be a bigger delay as I sort out one idea that has been requested several times. I want to add some floating point stuff, but to do that I need to write support for that for LaTeX3. I have some ideas, but it will take a while to actually do the work.
