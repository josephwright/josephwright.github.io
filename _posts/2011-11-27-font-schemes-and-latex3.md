---
title: Font schemes and LaTeX3
layout: post
permalink: /2011/11/27/font-schemes-and-latex3/
categories:
  - LaTeX3
tags:
  - fonts
  - NFSS
  - OpenType
---
There was a [question recently](https://tex.stackexchange.com/q/36112/73) on the [TeX.sx](https://tex.stackexchange.com/) site about font selection and LaTeX3. At the moment, there is not a LaTeX3 font system set up, and there are issues outstanding, so this is not something with a single answer. What I can do, though, is look at what seems likely and what some of the areas to consider are.

## (New) Font Selection Scheme

TeX's font mechanism is pretty basic. There is no relationship between one text font and another: they are all simply set up using the `\font` primitive. So with plain TeX

```latex
{\bf Some {\it text}}
```

will have 'Some' in bold, but 'text' in mid-weight italics. LaTeX2e introduced the 'New Font Selection Scheme' (NFSS), which provides a method for managing fonts in a way that is likely to be more logical for the user. Thus

```latex
{\bfseries Some {\itshape text}}
```

will have the inner text both bold and italic. At the same time, the NFSS provides a system for loading font files in an organised way and substituting fonts when a particular shape combination is unavailable.

Over all, the NFSS is one the key successes of LaTeX2e compared with LaTeX2.09. There are also a lot of existing `.fd` files about for using fonts with LaTeX2e, and supporting those is important. So something like the NFSS is definitely needed: the 'New' is rather anachronistic nowadays, so the working title is just FSS.

The NFSS is not perfect, and so LaTeX3's FSS cannot be simply a clone of NFSS. Perhaps the most common complaint about the NFSS is that `\textsc` is treated as a shape, which makes it impossible to combine it with `\itshape` to have italic small caps. Other areas which need addressing are for example flexible sizing and proportional/fixed width numbers for tables. This is all evolutionary, and so the plan is to port the existing NFSS first, tidy it up to fit better with LaTeX3 coding approaches, then add new abilities.

## Font face loading

The second area to think about is loading fonts in the first place. The traditional LaTeX2e approach to this to set up a small(ish) package to select a font family, for example [lmodern](http://ctan.org/tex-archive/fonts/lm) or [`mathptmx`](https://ctan.org/pkg/mathptmx), which will then use the NFSS to load the appropriate TeX font files. For users of XeTeX or LuaTeX, the standard method is to use the [`fontspec`](https://ctan.org/pkg/fontspec) package, which provides an interface between the extended `\font` primitives in these engines and the NFSS.

There are a few things to think about here. First, while XeTeX and LuaTeX can load system fonts directly, pdfTeX cannot. Secondly, even if you are using XeTeX or LuaTeX access to traditional TeX fonts cannot be ignored. There is a lot of MetaFont material on CTAN which is not available in any other format, so simply dropping support for these is not an option.

What I feel we need is a single font-loading interface at the user level which is capable of dealing with these requirements. Clearly, `fontspec` is going to provide inspiration on how to proceed, but some mechanism for working with pdfTeX will also be needed. My personal take on this is we'll need a mapping layer, which will mean that at the user level you choose a font by name (as you would in a GUI application), and which then does the appropriate translation to the engine layer.

There are also math mode fonts to worry about. OpenType maths fonts are very much in development, but that doesn't help with pdfTeX and again does not cover all cases. So again we need to continue to support TeX's traditional math mode fonts. That will probably be the last part of this particular jigsaw to be tackled, simply because it's the one with the least clear path at present.
