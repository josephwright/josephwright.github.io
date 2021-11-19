---
title: "LaTeX3: xparse"
layout: post
permalink: /2009/06/16/latex3-xparse/
categories:
  - LaTeX3
tags:
  - xparse
---
The next step for [LaTeX3](https://www.latex-project.org/latex3.html) development is to revise the two existing `xpackages` which are available to make a link between the code level and the user: `xparse` and template. Of the two, the `xparse` package is by far the easier to understand.

In LaTeX2e, you can either use the LaTeX method to create new commands:

<!-- {% raw %} -->
```latex
\newcommand*\mycommand[2][]{%
  code goes here, using #1 and #2
}
```
<!-- {% endraw %} -->

or you can do things yourself using a mixture of TeX primitives and LaTeX internal functions (and ignoring the issue of default value):

<!-- {% raw %} -->
```latex
\def\mycommand{%
  \@ifnextchar[{%
    \@mycommand
  }{%
    \@mycommand[]%
  }%
}
\def\@mycommand[#1]#2{%
  code goes here, using #1 and #2
}
```
<!-- {% endraw %} -->

This does not make for code which is easy to alter to reflect different input syntax (for example XML), or to change internal functions without knowing how the user input works. The idea of `xparse` is to separate out the user syntax from the internal code. Currently, exactly what tools need to be available is still being decided. The current version of `xparse` would expect the following syntax:

```latex
\DeclareDocumentCommand \mycommand { o m } {
  code goes here, using #1 and #2
}
```

The idea is that each argument is represented by a letter, for example `o` for an optional argument, `m` for a mandatory one or `s` for an optional star. This makes it possible it see immediately from the definition how many arguments are needed (one for each letter). It also means that the internal functions, which implement things, can be separated totally from the user part of the system. In that way, internal functions can have a fixed number of arguments, and leave `xparse` to supply them. So if the internal function needs to be changed, it does not matter how it is used, or _vice versa_.

That all sounds very good, but there are some outstanding issues. For example, handling verbatim arguments is not straight-forward. There are a couple of possible approaches to this. Either stick to a simple system, and accept that not everything can be done in the same way, or make the system more flexible but complicated. I'm currently in favour of the first approach: almost every user function is simple (especially as we have the e-TeX extensions and so can `\scantokens` our way out of a lot of problems). I'd be interested to hear what other people think would be useful.
