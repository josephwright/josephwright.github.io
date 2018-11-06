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
In my <a href="https://www.texdev.net/2012/08/25/exploring-chemfig-basics/">previous post</a>, I looked at the basics of using the <a href="http://ctan.org/pkg/chemfig">ChemFig</a> package to create chemical structures. I finished that post with a structure that is complete but which I think does not look great compared with the reference version I created in <a href="http://www.cambridgesoft.com">ChemDraw</a>. (There's a MyChemistry entry that looks at similar customisation: worth a look!)

<h2>Atom placement</h2>

The first issue to tackle is the placement of atom labels. ChemFig 'detects' atoms, so that the labels are correctly centred relative to bonds. However, that does not work with numbered R-groups, as the numbers need to be 'ignored' for alignment purposes. This is a pretty common requirement, so ChemFig provides a way to 'split' labels, using <code>|</code>:

<pre><code>\chemfig{
  *6(-(-R|^2)=-
    (-=[::-60]N-*6(=(-R|^3)-=(-R|^4)-=(-R|^3)-))
  =(-OH)-(-R|^1)=)
}
</code></pre>

which gives the output

<img class="alignnone size-medium wp-image-1919" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig6-300x171.png" alt="" width="300" height="171" />

To see the difference here, look at for example R<sup>2</sup> here compared to the version in the previous post: it's subtle, but it is there!

<h2>Atom spacing and bond width</h2>

The standard settings for ChemFig share a 'feature' with those for ChemDraw: they don't look very good! As I said in the previous post, I use the Royal Society of Chemistry's template for my structures, as I think they look much better. The template uses 7 pt text, and so the lengths, <em>etc.</em> all match that size. For use in LaTeX, I want things to be more flexible so wanted to convert the values into em (<em>i.e.</em> relative dimensions based on font size).

There are three key dimensions used by both ChemDraw and ChemFig to set how bonds look: the bond length, the line width and the gap between lines when drawing double bonds. There is also a 'margin' used between atom labels and bonds, so the two don't touch. After a bit of work doing the calculation (using to the <a href="https://github.com/latex3/svn-mirror/blob/master/l3kernel/l3fp.dtx">LaTeX3 FPU</a>), I found that

<pre><code>\setdoublesep{0.35700 em}  % 'Bond Spacing'
\setatomsep{1.78500 em}    % 'Fixed Length'
\setbondoffset{0.18265 em} % 'Margin Width'
\newcommand{\bondwidth}{0.06642 em} % 'Line Width'
\setbondstyle{line width = \bondwidth}
</code></pre>

was the right set up. The comments are the ChemDraw names for settings, and I've set the line width as a command as it turns out I'll want it again for some more advanced things to be covered in the next post.

<img class="alignnone size-medium wp-image-1920" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig7-300x169.png" alt="" width="300" height="169" />

<h2>The central double bond</h2>

Changing the bond spacing shows up another issue: the central double bond is not right. Rather than bond to the 'middle' of the double bond, we want the chain to choose one 'side'. That can be done using either <code>_</code> or <code>^</code>, depending on which side is required. I decided to match the ChemDraw version using

<pre><code>\chemfig{
  *6(-(-R|^2)=-
    (-=^[::-60]N-*6(=(-R|^3)-=(-R|^4)-=(-R|^3)-))
  =(-OH)-(-R|^1)=)
}
</code></pre>

<img class="alignnone size-medium wp-image-1921" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig8-300x169.png" alt="" width="300" height="169" />

<h2>Atom font</h2>

The final thing to adjust to get this example right is the font used for atom labels: the convention is to use sanserif. ChemFig prints text using the <code>\printatom</code> command, which is set up to ensure math mode and <code>\mathrm</code>. Thus the simplest approach is

<pre><code>\renewcommand*{\printatom}[1]{\ensuremath{\mathsf{#1}}
</code></pre>

Like many people, I use the excellent <a href="http://ctan.org/pkg/mhchem"><code>mhchem</code></a> to write in-line chemical equations, so I wanted to use the <code>\ce</code> (or faster <code>\cf</code>) command for printing atoms. My initial attempt failed, with an internal error. A quick e-mail to the ChemFig author led to a fix

<!-- {% raw %} -->
<pre><code>\makeatletter
\def\CF@node@content{%
  \expandafter\expandafter\expandafter
    \printatom\expandafter\expandafter\expandafter
      {\csname atom@\number\CF@cnt@atomnumber\endcsname}%
    \ensuremath{\CF@node@strut}%
}
\makeatother
</code></pre>
<!-- {% endraw %} -->

followed by

<pre><code> \renewcommand*{\printatom}[1]{{\sffamily\cf{#1}}}
</code></pre>

leads to the final input

<!-- {% raw %} -->
<pre><code>\documentclass{article}
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
</code></pre>
<!-- {% endraw %} -->

and output

<img class="alignnone size-medium wp-image-1922" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig9-300x173.png" alt="" width="300" height="173" />

I'd say that is pretty good: I'd be happy to use this in a publication (although drawing the kind of structures I do my research with would be a challenge!).

In the final part of this series, I'm going to look at some other things that are needed for chemical structures but which don't show up in the demo I've used. We'll see that many can be done, but there will be one or two outstanding challenges.
