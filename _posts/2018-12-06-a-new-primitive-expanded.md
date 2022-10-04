---
title: "A 'new' primitive: \\expanded"
layout: post
permalink: /2018/12/06/a-new-primitive-expanded
categories:
  - General
---

In recent years, development of pdfTeX has been very limited, with the v1.40
branch now being around for over 10 years. However, in the past there were
plans for a v1.50 branch, and some code was actually written. One primitive
that was fully coded-up at that time was `\expanded`. The idea of this is
pretty simple: it carries out full expansion like `\message` (and _almost_
like `\edef`), but it is still expandable. For example, try

```latex
\def\a{\b}\def\b{c}
\message{Hello \a\space #}
\detokenize\expandafter{\expanded{Hello \a\space #}}
\bye
```

using LuaTeX.

Why is the example for LuaTeX? When LuaTeX development started, the team
behind it used the development code from pdfTeX as a starting point, and that
included `\expanded`. However, release pdfTeX itself didn't incorporate this
code, and so it's not been more widely available.

## Enter the LaTeX Team

For some time, the [LaTeX Team](https://www.latex-project.org/) have been
thinking about asking for `\expanded` to be made more widely available. Unlike
the [`\romannumeral` 'trick'](/2011/07/05/expansion-using-romannumeral),
`\expanded` does not require any hard work to get 'past' any output, so it is
very useful for creating macros that work like functions. It's also fast and
clear in intention.

In the past, making requests for changes to the pdfTeX codebase was hard as
building and testing is non-trivial. However, nowadays there is a [GitHub
repo](https://github.com/TeX-Live/texlive-source) which is also set up for
[Travis-CI](https://www.travis-ci.com). That means that there is an easy
way to test: set up an Ubuntu virtual machine, clone the repo there, and run
the tests in the same way Travis-CI does.

With that handy set up available, I sat down (on behalf of the team) and did
the hard work: a bit of copy-pasting! As well as pdfTeX, I worked out how to
add `\expanded` to [XeTeX](http://xetex.sourceforge.net/) and the Japanese
TeX engines pTeX and upTeX. After a bit of discussion, this code has been
accepted by [TeX Live](https://tug.org/texlive/), and will be there in
the 2019 release.

## Get it now

For those people who want to test now, LuaTeX of course has `\expanded`, so it
is easy to try out. For [MiKTeX](https://miktex.org) users, Christian Schenk
has already updated all of the binaries, so a quick update will give pdfTeX
and XeTeX with `\expanded`. For TeX Live users, binary updates only happen
once a year. But if you want to grab something now, you could look for example
at [W32TeX](http://www.w32tex.org/) (which is the source for Windows binaries
in TeX Live): you'll have to manually rebuild your formats, but if you know
enough to want to test, you probably understand that instruction!

## Using `\expanded`

The team have already started planning to use `\expanded`, and recently
added a new expansion type to [`expl3`](https://ctan.org/pkg/l3kernel):
`e`-type. We have some emulation code that allows this to work (slowly)
even with older binaries. I'd expect us to make heavy use of this in new
functions: it's a _lot_ easier than the `\romannumeral` approach.
