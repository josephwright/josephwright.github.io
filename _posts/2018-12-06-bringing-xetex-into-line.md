---
title: Bringing XeTeX into line
layout: post
permalink: /2018/12/06/brining-xetex-into-line
categories:
  - General
tags:
  - XeTeX
---

In parallel with work on the
[`\expanded`primitive](/2018/12/06/a-new-primitive-expanded), I've been working
recently on bringing the 'utility' primitives in
[XeTeX](https://sourceforge.net/projects/xetex/) into line with those in
pdfTeX, pTeX and upTeX.

## Background

XeTeX was written to extend e-TeX to allow full Unicode working, including
loading system fonts. The development started from the DVI-mode e-TeX, rather
than from pdfTeX, which had added various new primitives to e-TeX. Much of
the difference between pdfTeX and e-TeX is directly to do with producing
PDF output, but there are some additions that are entirely independent of
that.

Over the years, some of the 'utilities' have been added to XeTeX (for example
`\pdfstrcmp`, which in XeTeX is just `\strcmp`). However, several have not made
it, but _have_ been added to pTeX and upTeX. That's meant that XeTeX has between
'a bit behind' in feature terms: there are things that simply can't be done
without primitive support.

## An opportunity arises

As [I've said](/2018/12/06/a-new-primitive-expanded) in my other post today,
the recent setting up of a [Travis-CI](https://travis-ci.com) testing
environment for [TeX Live](https://tug.org/texlive/) building means that it
is now _easy_ to try adding new material to the
[WEB](https://en.wikipedia.org/wiki/WEB) sources of pdfTeX, XeTeX,
_etc._ As I was working on `\expanded` anyway, I decided that I'd look at
bringing XeTeX back 'into line' with pTeX and upTeX. That's important as
for [`expl3`](https://ctan.org/pkg/l3kernel), the
[LaTeX team](https://www.latex-project.org) have been using almost all
of the primitives that were 'missing' in XeTeX.

## The new features

So what has been added? The new additions are all named without the
`pdf` part that pdfTeX includes, as they have nothing to do with PDFs:

- `\creationdate`
- `\elaspsedtime`
- `\filedump`
- `\filemoddate`
- `\filesize`
- `\resettimer`
- `\normaldeviate`
- `\uniformdeviate`
- `\randomseed`

These enable things like random numbers in the LaTeX3 FPU, [measuring
code performance](https://www.latex-project.org/news/2018/10/28/benchmarking/)
and checking the details of files: all stuff that is in `expl3` and will now
work with XeTeX.

## One more thing

As well as the above, I made one other minor adjustment to XeTeX: altering
how `\Ucharcat` works so it can create category code 13 ('active') tokens.
That probably won't show up for users except it helps the team extend some
low-level `expl3` code. Hopefully it will mean there is on fewer XeTeX
restriction.

## Getting the code

TeX Live only gets binary updates once per year, so users there will need to
wait for the 2019 release. On the other hand, [MiKTeX](https://miktex.org)
already has the new features, so if you are on Windows it's pretty trivial
to try out. If you use TeX Live and really want to test out, you can update
your binaries in-place, for example from [W32TeX](http://www.w32tex.org): if
you understand what that means, you probably know how to do it!
