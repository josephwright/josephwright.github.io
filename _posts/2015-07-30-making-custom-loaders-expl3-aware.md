---
title: Making custom loaders expl3-aware
layout: post
permalink: /2015/07/30/making-custom-loaders-expl3-aware/
categories:
  - expl3
tags:
  - expl3
---
The `expl3` syntax used by the developing programming layer for LaTeX3 is rather different from 'traditional' TeX syntax, and therefore needs to be turned on and off using the command pair `\ExplSyntaxOn`/`\ExplSyntaxOff`. In package code making use of `expl3`, the structure

```latex
\ExplSyntaxOn % Or implicit from \ProvidesExplPackage
....
\usepackage{somepackage}
....
\ExplSyntaxOff % Or the end of the package
```

will switch off `expl3` syntax for the loading of `somepackage` and so will work whether this dependency uses `expl3` or not.

This is achieved by using the LaTeX2e kernel mechanism `\@pushfilename`/`@popfilename`, which exists to deal with the status of `@` but which is extended by `expl3` to cover the new syntax too. However, this only applies as standard to code loaded using `\usepackage` (or the lower-level kernel command `\@onefilewithoptions`). Some bundles, most notable [Ti<em>k</em>Z](https://ctan.org/pkg/pgf), provide their own loader commands for specialised files. These can be made '`expl3`-aware' by including the necessary kernel commands


<!-- {% raw %} -->
```latex
\def\myloader#1{%
  \@pushfilename
  \xdef\@currname{#1}%
  % Main loader, including \input or similar
  \@popfilename
}
```
<!-- {% endraw %} -->

For packages which also work with formats other than LaTeX, the push and pop steps can be set up using `\csname`

<!-- {% raw %} -->
```latex
\def\myloader#1{%
  \csname @pushfilename\expandafter\endcsname
  \expandafter\xdef\csname @currname\endcsname{#1}%
  % Main loader, including \input or similar
  \csname @popfilename\endcsname
}
```
<!-- {% endraw %} -->

Of course, that will only work with LaTeX (the stack is not present in plain TeX or ConTeXt), but as the entire package idea is essentially a LaTeX one that should be a small problem.
