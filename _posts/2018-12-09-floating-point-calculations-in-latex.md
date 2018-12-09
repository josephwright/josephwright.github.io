---
title: Floating point calculations in LaTeX
layout: post
permalink: /2018/12/09/floating-point-calculations-in-latex
categories:
  - LaTeX
tags:
  - FPU
---

TeX does not include any 'native' support for floating point calculations, but
that has not stopped lots of (La)TeX users wanting to do sums (and more
complicated things) in their document. As TeX is [Turing
complete](https://en.wikipedia.org/wiki/Turing_completeness), it's not a
surprise that there are several ways to implement calculations. For end users,
the differences between these are not important: what is key is what to use.
Here, I'll give a bit of background, look at the various possibilities, then
move on to give a recommendation.

## Background

When Knuth wrote TeX, he had one aim in mind: high-quality typesetting. He also
wanted to have sources which were truly portable between different systems. At
the time, there was no standard for specifying how floating point operations
should be handled at the hardware level: as such, no floating point operations
were system-independent.

Knuth decided that TeX would provide no user access to anything dependent on
platform-specific floating-point operations. That means that the TeX functions
that look like floats (in particular dimen work) actually use _integer_
arithmetic and convert 'at the last minute'.

## Technical considerations

There are two basic approaches to setting up floating point systems in TeX:
either use dimensions or doing everything in integer mathematics.

Using dimensions, the input range is limited and the output has restricted
accuracy. But on the other hand, many calculations are quite short and they
are fast. On the other hand, if everything is coded in integer mathematics,
the programmer can control the accuracy completely, at the cost of speed.

Although it's not an absolute requirement, e-TeX does make doing things a bit
easier: rather than having to shuffle everything a piece at a time, it is
possible to use inline expressions for quite a lot of the work.

Another key technical aspect is expandablity. This is useful for some aspects
of TeX work, particularly anywhere that it 'expects a number': only expansion
is allowed in such places.

One other thing to consider is handling of TeX registers as numbers. Converting
for example a length into something that can be used in a floating point
calculation is handy, and it matches what e-TeX does in for example `\intexpr`.
But in macro code it has to be programmed in.

## Functionality

The other thing to think about here is functionality: what is and isn't needed
in terms of mathematics. Doing straight-forward arithmetic is obviously
easier than working out trigonometry, logarithms, _etc._ What exactly you need
depends on the use case, but obviously more functionality is always better.

## (Package) options

For simple work using the dimen approach is convenient and fast: it takes
only a small amount of work to set up stripping off the `pt` part. I'm writing
here for people who don't want to delve into TeX innards, so let's assume
a pre-packaged solution is what is required.

There are lots of possible solutions on [CTAN](https://www.ctan.org) which
cover some or all of the above. I don't want to get into a 'big list', so
I'll simply note here that the following are available:

- [`apnum`](https://ctan.org/pkg/apnum)
- [`calculator`](https://ctan.org/pkg/calculator)
- [`fltpoint`](https://ctan.org/pkg/fltpoint)
- [`pst-fp`](https://ctan.org/pkg/pst-fp)
- [`minifp`](https://ctan.org/pkg/minifp)
- [`realcalc`](https://ctan.org/pkg/realcalc)
- [`xint`](https://ctan.org/pkg/xint)

Some of these have variable or arbitrary precision, others work to a
pre-determined level, and they also vary in terms of functions covered,
expandablity and so on.

I want to focus in on three possible 'contenders':
[`fp`](https://ctan.org/pkg/fp), [`pgf`](https://ctan.org/pkg/pgf)
and the [LaTeX3 FPU](https://ctan.org/pkg/xfp). The `fp` package formally
uses _fixed_ not _floating_ point code, but the key for us here is that it
allows a wide range of high-precision calculations. It's also been
around for a _long_ time.  However, it's quite slow and doesn't have convenient
expression parsing (it does reverse Polish).

On the flip side, the mathematics engine in `pgf` uses dimens internally, so
it is (relatively) fast but is limited in accuracy. The range limits also
show up in some unexpected places, as a lot of range reduction is needed to make
everything work. On the other hand, `\pgfmathparse` does read 'normal'
mathematical expressions, so it's pretty easy to use.

The LaTeX3 FPU is part of [`expl3`](https://ctan.org/pkg/l3kernel), but is
available nowadays as a document-level package
[`xfp`](https://ctan.org/pkg/xfp). In contrast to both `fp` and the `pgf`
approach, the LaTeX3 FPU is expandable. Like `pgf`, using the FPU means
we can use expressions, and we also get [reasonable
performance](https://tex.stackexchange.com/q/463554) (Bruno Le Floch worked
hard on this aspect). The other thing to note is that the FPU is intended to
match behaviour specified in the [IEEE
754](https://en.wikipedia.org/wiki/IEEE_754) standard, and that the team have
a set of tests to try to make sure things work as expected.

There's one other option that one must consider: Lua. If you address
only using LuaTeX, you can happily break out into Lua and use it's ability
to use the 'real' floating point capabilities of a modern PC. The one
wrinkle is that without a bit of work, the Lua code _doesn't_ know about
TeX material: registers and so on need to be pre-processed. It also goes
without saying that using Lua means being tided to LuaTeX!

## Recommendation

As you can see above, there are several options. However, for end users
wanting to do calculations in documents I think there is a clear best
choice: the LaTeX3 FPU.

```latex
\documentclass{article}
\usepackage{xfp}
\begin{document}
\fpeval{round(sqrt(2) * sind(40),2)}
\end{document}
```

You'd probably expect me to say that: I am on the [LaTeX
team](https://www.latex-project.org/). But that's not the reason. Instead,
it's that the FPU is almost as fast as using dimens (see `pgf` benchmarking),
but offers the same accuracy as a typical GUI application for maths. It also
integrates into normal LaTeX conventions with no user effort.
