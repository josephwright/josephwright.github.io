---
title: "biblatex v1.1: dynamic reference sets"
layout: post
permalink: /2011/01/06/biblatex-v1-1-dynamic-reference-sets/
categories:
  - biblatex
  - Packages
---
The latest version of [`biblatex`, v1.1,](https://ctan.org/pkg/biblatex) appeared on [CTAN](https://www.ctan.org) yesterday. This is a feature release, not just bug fixes, and so there are lots of new things there. At the same time, [Biber](http://biblatex-biber.sourceforge.net/) has been updated to v0.7. If you use [TeX Live 2010](https://tug.org/texlive), you'll be able to get the new `biblatex` using `tlmgr` in a day or so, and can get the Biber update _via_ [TLcontrib](http://tlcontrib.metatex.org/) already.

Many of the new features rely on Biber, and will not work with BibTeX. As Biber has lots of advantages anyway, including UTF-8 support and active development, this is no real hindrance.

I want to focus here on one new feature, as it's one I requested. In chemistry and physics we tend numerical reference styles and to have lots of references. Often, several of these will be related, and so can be 'compacted' into a single number. With traditional BibTeX styles, this can be done using the `mciteplus` package and a suitable `.bst` file. `biblatex` has supported this using 'reference sets' for some time, but up to now this has required modification of the database entries. In v1.1, you can define a reference set in the preamble:

```latex
\defbibentryset{set1}{key1,key2,key3}
```

and then cite the set in the document. There is also support for `mciteplus-`like syntax, but I think it's probably best to use the native `biblatex` approach here.

Compressing multiple citations in a dynamic way was really the only problem I had with using `biblatex` for all of my citations. Now that this is sorted, I'll be sticking to `biblatex` all of the time, and I'd urge other physical scientists to do the same: `biblatex` is a much more flexible approach than the traditional BibTeX citation system.
