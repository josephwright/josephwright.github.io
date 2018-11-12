---
title: Fixing LaTeX2e
layout: post
permalink: /2014/12/28/fixing-latex2e/
categories:
  - General
---
When LaTeX2e was first released in 1994 a lot of work had been done to avoid breaking existing LaTeX2.09 documents but allowing changes such as the package and font selection systems. The stability of LaTeX as demonstrated by that approach is one reason it's been a success. However, there is also a need to allow for change: the world does not stand still. While the LaTeX2e kernel is not about to alter radically, the team are looking to address some areas where the needs today mean that change (or at least adaptation) is the right approach. David Carlisle [talked about this](https://vimeo.com/113430065) at the UK-TUG meeting in November: here I'm going to try to look at the same issues in my own way. An important note before I start: the fixes I'm talking about here are all important but they are not about to change LaTeX2e into something else!

## Kernel modifications

Over the years various bugs and  issues have come up in the LaTeX2e kernel. Out-and-out bugs get fixed, but issues which are more about 'code design' are more tricky. There's a tension between sorting these out and having the kernel 'stable', so not altering existing documents at all. The approach the team have taken to this to date is a package called `fixltx2e`. It contains ideas that really should go into the kernel but haven't as they might alter existing documents. The idea is then that most people should really use these fixes in the form

```latex
\RequirePackage{fixltx2e}
\documentclass...
```

The problem: most people don't do that, or load `fixltx2e` half-way through a preamble, or use it with packages that were not tested both with and without the fixes. That's not a great position.

What we are looking at now is moving to a situation where the fixes _are_ in the kernel as standard but with a mechanism to back them out. The details still need to be finalised, but the general plan is that once we make the change people will get the fixes without needing to take any action. If a document really has to be completely unchanged we'll provide an 'undo' package with a way of setting the date that the kernel should be rolled-back to: that way you'll be able to say 'I always want the kernel as it was on ... even if any fixes at all are made later'. We hope that will be a good balance.

## Register allocation

Classical TeX provides 256 registers of each type. That limit was raised by the e-TeX extensions, which were finalised in 1999 and give us 32768 of the main register types (more on that nuance in a bit). While the team have used the extensions for many years in some packages, the LaTeX kernel itself still uses the classical TeX allocation system. That means that you can run into the

```latex
No room for a new ....
```

error even though there is lots of space. Loading the `etex` package

```latex
\RequirePackage{etex}
\documentclass...
```

modifies the allocation system to use those extra registers, but a lot of non-expert users don't know this. So again we have a situation where a change in the kernel is the best plan.

What we are looking at here is what is the obvious solution: extending the register allocators in the LaTeX2e kernel 'out of the box' as long as the e-TeX extensions are available. That should be a transparent change for almost everyone, and will still allow `etex` to be loaded.

One minor wrinkle is inserts. e-TeX doesn't extend how many inserts TeX has: there are still only 256. LaTeX2e doesn't actually need many inserts as floats are handled without them (or without needing one insert per float), but at present the code for making floats does allocate inserts. The best solution here is to change what the kernel does so it no longer uses `\newinsert` to make floats: that will let us provide more float storage with basically no 'cost'.

## Unicode Engines

The Unicode engines XeTeX and LuaTeX have been with us for a few years now, and quite a lot of what they need to do at the format level is well-established. At the moment, the format-building routines make some changes 'around' the core `latex.ltx` file to accommodate these requirements: the code supplied by the team doesn't 'know' about these newer engines. We're therefore looking to address that by adding some conditional code.

The first area to tackle overlaps with the point above: LuaTeX extends the register allocation again beyond e-TeX, while XeTeX needs an allocator for `\XeTeXinterchartoks`. Both of these can readily be added to an updated allocation system.

The bigger impact of Unicode engines is that they have a different requirement from 8-bit engines in setting up the codes TeX uses for case changing. The LaTeX2e kernel sets up the `\lccode` and `\uccode` for the 8-bit range and assumes `T1` encoding. With the newer engines, that's not really great as they use Unicode code points and (almost certainly) Unicode (`EU1`/`EU2`) encodings. The format builders alter these assumptions using something of a hack, so we are looking to add the appropriate conditionals to the format itself. For end users that won't really show, but it will mean that the format itself will be 'in control' here: something we are keen to work on.

## LuaTeX extras

As well as the issues it shares with XeTeX, LuaTeX introduces ideas such as Lua callbacks and `\attribute` allocation. These areas are still somewhat 'in flux': the team currently feel that we need to get some consensus from the community (particularly active package authors) before adding anything here. However, it's important that we get people thinking.

## Conclusions

The changes we are looking at for LaTeX2e should help keep things 'ticking over' in the kernel will help us keep things working and offer some new abilities to end users. At the same time, they should move more of the kernel people see 'in the wild' back into the control of the team: something we are keen on as we need to be able to fix the bugs. We're hoping to check in the code for these changes soon: expect requests for testing!
