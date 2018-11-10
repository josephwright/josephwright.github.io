---
title: Tracking chemical compounds with chemcompounds
layout: post
permalink: /2010/07/25/tracking-chemical-compounds-with-chemcompounds/
categories:
  - General
tags:
  - chemcompounds
  - chemistry
---
As a chemist, one of the things I want to do is track compound numbers (which are normally given as bold numbers, **1**, **2**, _etc_.). The traditional way to do that is by hand, which works but does require some concentration. Recent versions of [ChemDraw](http://www.cambridgesoft.com/) have included an add-in for Word to do things automatically, and of course there is LaTeX support for the same idea.

In LaTeX there is a choice between two packages for tracking what is what. First, there is the [`bpchem`](https://ctan.org/pkg/bpchem) package. It provides for the idea of subdivisions, so you can have **1a**, **1b**, **1c** and so forth. However, I find the interface in `bpchem` is a bit awkward. The alternative is the [`chemcompounds`](https://ctan.org/pkg/chemcompounds) package. It has a very easy to use approach to tracking, but does not have built-in support for subdivisions. So I've been working on how to achieve this easily in some stuff I'm writing at the moment. It turns out to be quite easy when you think about it.

The first stage is of course to load the package.

```latex
\usepackage[noimplicit]{chemcompounds}
```

I've decided to go with the option to turn off automatically creating new compound references, which means I have to declare each one separately. This requires a block of declarations in the preamble, but I actually find this easier than doing things _ad hoc_. The subdivisions I want are all about R groups (chemists will understand!). So I've started by setting up some simple R group letters (I have a family of compounds, and so it makes sense to use the same letter for the same R group in each case):

```latex
\declarecompound[a]{Mes}
\declarecompound[b]{iPr}
```

Hopefully you can see how this works: the optional argument sets up the label that will print, and the mandatory one is the label I'll use to refer to the compound.
Then I need to set up the general compounds (the ones that will be **1**, **2** and so on). I can let `chemcompounds` do the numbering, so this is easy:

```latex
\declarecompound{imidazole}
\declarecompound{pincer:salt}
\declarecompound{pincer:carbene}
```

The last stage in the preamble is to create the subdivided compounds. Rather than have to track the numbers and letter myself, I've found that I can simply refer back to the existing labels:

```latex
\declarecompound[\compound{imidazole}\compound{Mes}]
  {imidazole:Mes}
\declarecompound[\compound{imidazole}\compound{iPr}]
  {imidazole:iPr}
\declarecompound[\compound{pincer:salt}\compound{Mes}]
  {pincer:salt:Mes}
\declarecompound[\compound{pincer:salt}\compound{iPr}]
  {pincer:salt:iPr}
\declarecompound[\compound{pincer:carbene}\compound{Mes}]
  {pincer:carbene:Mes}
\declarecompound[\compound{pincer:carbene}\compound{iPr}]
  {pincer:carbene:iPr}
```

In the document body, things are now very easy. I just use the `\compound` macro. So for the general case I'll have

```latex
\compound{imidazole}
```

(printing say **4**) whereas for a single case I might have

```latex
\compound{imidazole:Mes}
```

(printing say **4a**). This keeps my source easy to follow (I don't have to remember numbers and letters, only labels), and avoids mistakes on my part.
