---
title: "ConTeXt in TeX Live"
layout: post
permalink: /2025/06/08/context-in-tex-live
categories:
  - general
---

[ConTeXt](https://www.pragma-ade.nl/index.htm) has traditionally had a somewhat
different distribution approach to other TeX code. The ConTeXt developers
provide a [stand-alone installer](https://www.pragma-ade.nl/install.htm) which
provides the macro and Lua code which make up ConTeXt, the binaries which are
needed and fonts in a predictable way. This self-contained approach makes it
easier to ensure that macros, Lua and binaries are all matched up.

A version of ConTeXt does go into [TeX Live](https://www.tug.org/texlive/), but
to date that's been a once-a-year change with some non-trivial work to match up
with how TeX Live works. That's now changed: [Max
Chernoff](https://github.com/gucci-on-fleek) has set up a [scripted
approach](https://github.com/gucci-on-fleek/context-packaging) which
automatically does the work and means that ConTeXt in TeX Live will now only
be a day or two behind the official release.

This will be really useful for anyone working with mixed TeX formats (ConTeXt,
LaTeX, plain, OpTeX), as they'll not have to worry if they are using ConTeXt
from TeX Live or from the standalone. It also means it will be easier to test
other TeX code against current ConTeXt just by using a single standard setup.
That should be good for example for testing generic
[`expl3`](https://ctan.org/pkg/l3kernel) loading in ConTeXt, something we've
[worked on recently](https://github.com/latex3/latex3/issues/1724).
