---
title: "The mythical LaTeX3"
layout: post
permalink: /2024/11/11/the-mythical-latex3
categories:
  - expl3
---

When the [LaTeX Project team](https://www.latex-project.org) took over
maintenance of LaTeX from [Leslie
Lamport](https://www.microsoft.com/en-us/research/people/lamport/), LaTeX2e was
planned as an intermediate release to resolve immediate issues with the
then-current LaTeX2.09. The 'e' (or properly ε) was meant to indicate a small
change from LaTeX2.09, with longer-term plans centred on LaTeX3. As we know,
that proved rather hopeful, and we are still using LaTeX2e today: at least,
that's how it still announces itself.

## The 1990s plans

The plans for LaTeX3 developed by the team in the early 1990s envisaged
reimplementing LaTeX with a much cleaner underlying programming framework and
well-defined separation of user interface, design functions and programming. A
lot of these ideas were prototyped very early on, with a version of the
programming layer created well before LaTeX2e was finalised. But performance
was the big issue: yes, you could test things as a developer, but that was
basically it. At the same time, some ideas were not fully ready: before e-TeX
(pdfTeX extensions, _etc._), there was less that the engine could do, and
whilst Knuth's TeX is an excellent piece of software, the LaTeX3 ideas pushed
it to the limit.

So LaTeX2e was released in 1994, and development focussed on packages for many
years. That meant that 'LaTeX3' became something of an amusing idea: talked
about but with no likelihood of (visible) delivery.

## Development into the 2010s

Development of 'LaTeX3' ideas never stopped, of course: it was just that they
moved from being primarily targeting a new kernel to building on top pf
LaTeX2e. That results in a bundle called `l3in2e` and one called `xpackages` on
CTAN, although both were marked as experimental.

When I joined the LaTeX Project team in 2009, that's largely where things were.
However, the landscape had evolved: computers had become more powerful, e-TeX
and pdfTeX extensions to TeX were very widely available and development was
easier. That meant that LaTeX3 ideas, particularly the programming language
(`expl3`) was usable in real documents: the
[`fontspec`](https://ctan.org/pkg/fontsepc) package in particular was written
in `expl3` and was quite usable. I picked that up and wrote the second version
of [`siunitx`](jttps://ctan.org/pkg/siunitx) in `expl3`.

At the same time, some of my first work on the team was in getting `expl3` to
the point that the 'experimental' was no longer really true: you could use it
in a package and be happy that the code would continue to work between
releases. The other major task early in my team career was getting us into a
position that releases, first of `expl3` and then of the LaTeX2e kernel, were
easy to make from whatever platform we wanted: Linux, macOS and Windows.

Over the 2010s, this meant the team could round out ideas that had been
suggested first over 20 years before. Development was still as packages adding
on to the kernel, but `xparse` (document commands), `xtemplate` (flexible
document structures) and `xgalley` (a new approach to the main vertical list)
were all revised and testable.

## The 2020s: LaTeX2e 2020-02-02 and beyond

By 2020, work on the core idea of a programming layer had reached the point
that the code was stable and performant, and that the team wanted to be able to
rely on it for  kernel developments. So we took the step to integrate loading
`expl3` into the LaTeX2e kernel, with the rather cryptic description 'Improved
load times for `expl3`' in _LaTeX News_. Following that, `xparse` and
`xtemplate` have also been (largely) added to the kernel, tightening up the
parts that worked from those that do turn out to have been purely experiments.

With this functionality available, new ideas such as hook management and
re-implementation of older ones such as lists is possible: some of that is
currently only activated if you use `\DocumentMetadata` as a 'marker'. For
updated documents, that means many of the LaTeX3 ideas are being ued: the
programming layer, a way of making document commands (`\NewDocumentCommand`
originally from `xparse`) and templates (originally from `xtemplate` and used
to update list code, etc.).

There are also more subtle changes across the kernel, for example updating
commands to use UTF-8 everywhere, make more functions engine-robust, etc. Put
together, the 2024 LaTeX1e is quite different from the 1994 one: but you can
still rely on the long-term stability that's always been there.

## Conclusions

Whilst there will never be a stand-alone 'LaTeX3' format, the ideas that were
first explored by the LaTeX Project team in the early 1990s are now available
to users in the LaTeX kernel. They are being used to deliver an updated LaTeX
capable of producing accessible documents, and more widely to bring
customisation to the kernel. So whilst 'LaTeX3' might not eb something you'll
every say you use, if you use LaTeX, you are getting those features today.