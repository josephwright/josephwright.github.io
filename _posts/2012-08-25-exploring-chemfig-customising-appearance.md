---
id: 1493
title: 'Exploring ChemFig: Customising appearance'
date: 2012-08-25T17:18:23+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1493
permalink: /2012/08/25/exploring-chemfig-customising-appearance/
categories:
  - General
tags:
  - ChemFig
  - chemistry
  - tikz
---
In my [previous post](/2012/08/25/exploring-chemfig-basics/), I looked at the basics of using the [ChemFig](https://ctan.org/pkg/chemfig) package to create chemical structures. I finished that post with a structure that is complete but which I think does not look great compared with the reference version I created in [ChemDraw](https://www.cambridgesoft.com). (There's a MyChemistry entry that looks at similar customisation: worth a look!)

## Atom placement

The first issue to tackle is the placement of atom labels. ChemFig 'detects' atoms, so that the labels are correctly centred relative to bonds. However, that does not work with numbered R-groups, as the numbers need to be 'ignored' for alignment purposes. This is a pretty common requirement, so ChemFig provides a way to 'split' labels, using `|`:

```latex
\chemfig{
  *6(-(-R|^2)=-
    (-=[::-60]N-*6(=(-R|^3)-=(-R|^4)-=(-R|^3)-))
  =(-OH)-(-R|^1)=)
}
```

which gives the output

![](/wp-content/uploads/2012/08/ChemFig6-300x171.png)

To see the difference here, look at for example R<sup>2</sup> here compared to the version in the previous post: it's subtle, but it is there!

## Atom spacing and bond width

The standard settings for ChemFig share a 'feature' with those for ChemDraw: they don't look very good! As I said in the previous post, I use the Royal Society of Chemistry's template for my structures, as I think they look much better. The template uses 7 pt text, and so the lengths, _etc._ all match that size. For use in LaTeX, I want things to be more flexible so wanted to convert the values into em (_i.e._ relative dimensions based on font size).

There are three key dimensions used by both ChemDraw and ChemFig to set how bonds look: the bond length, the line width and the gap between lines when drawing double bonds. There is also a 'margin' used between atom labels and bonds, so the two don't touch. After a bit of work doing the calculation (using to the [LaTeX3 FPU](https://github.com/latex3/svn-mirror/blob/master/l3kernel/l3fp.dtx)), I found that

```latex
\setdoublesep{0.35700 em}  % 'Bond Spacing'
\setatomsep{1.78500 em}    % 'Fixed Length'
\setbondoffset{0.18265 em} % 'Margin Width'
\newcommand{\bondwidth}{0.06642 em} % 'Line Width'
\setbondstyle{line width = \bondwidth}
```

was the right set up. The comments are the ChemDraw names for settings, and I've set the line width as a command as it turns out I'll want it again for some more advanced things to be covered in the next post.

![](/wp-content/uploads/2012/08/ChemFig7-300x169.png)

## The central double bond

Changing the bond spacing shows up another issue: the central double bond is not right. Rather than bond to the 'middle' of the double bond, we want the chain to choose one 'side'. That can be done using either `_` or `^`, depending on which side is required. I decided to match the ChemDraw version using

```latex
\chemfig{
  *6(-(-R|^2)=-
    (-=^[::-60]N-*6(=(-R|^3)-=(-R|^4)-=(-R|^3)-))
  =(-OH)-(-R|^1)=)
}
```

![](/wp-content/uploads/2012/08/ChemFig8-300x169.png)

## Atom font

The final thing to adjust to get this example right is the font used for atom labels: the convention is to use sanserif. ChemFig prints text using the `\printatom` command, which is set up to ensure math mode and `\mathrm`. Thus the simplest approach is

```latex
\renewcommand*{\printatom}[1]{\ensuremath{\mathsf{#1}}
```

Like many people, I use the excellent [`mhchem`](https://ctan.org/pkg/mhchem) to write in-line chemical equations, so I wanted to use the `\ce` (or faster `\cf`) command for printing atoms. My initial attempt failed, with an internal error. A quick e-mail to the ChemFig author led to a fix


<!-- {% raw %} -->
```latex
\makeatletter
\def\CF@node@content{%
  \expandafter\expandafter\expandafter
    \printatom\expandafter\expandafter\expandafter
      {\csname atom@\number\CF@cnt@atomnumber\endcsname}%
    \ensuremath{\CF@node@strut}%
}
\makeatother
```
<!-- {% endraw %} -->


followed by

```latex
 \renewcommand*{\printatom}[1]{{\sffamily\cf{#1}}}
```

leads to the final input


<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage{chemfig}
\usepackage[version=3]{mhchem}
\makeatletter
\def\CF@node@content{%
  \expandafter\expandafter\expandafter
    \printatom\expandafter\expandafter\expandafter
      {\csname atom@\number\CF@cnt@atomnumber\endcsname}%
    \ensuremath{\CF@node@strut}%
}
\makeatother
\setdoublesep{0.35700 em}  % 'Bond Spacing'
\setatomsep{1.78500 em}    % 'Fixed Length'
\setbondoffset{0.18265 em} % 'Margin Width'
\newcommand{\bondwidth}{0.06642 em} % 'Line Width'
\setbondstyle{line width = \bondwidth}
\renewcommand*{\printatom}[1]{{\sffamily\cf{#1}}}
\begin{document}
\chemfig{
  *6(-(-R|^2)=-
    (-=^[::-60]N-*6(=(-R|^3)-=(-R|^4)-=(-R|^3)-))
  =(-OH)-(-R|^1)=)
}
\end{document}
```
<!-- {% endraw %} -->


and output

![](/wp-content/uploads/2012/08/ChemFig9-300x173.png)

I'd say that is pretty good: I'd be happy to use this in a publication (although drawing the kind of structures I do my research with would be a challenge!).

In the final part of this series, I'm going to look at some other things that are needed for chemical structures but which don't show up in the demo I've used. We'll see that many can be done, but there will be one or two outstanding challenges.
