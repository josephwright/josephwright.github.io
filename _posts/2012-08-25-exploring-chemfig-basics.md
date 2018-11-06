---
id: 1442
title: 'Exploring ChemFig: Basics'
date: 2012-08-25T16:08:21+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1442
permalink: /2012/08/25/exploring-chemfig-basics/
categories:
  - General
tags:
  - ChemFig
  - chemistry
  - tikz
---
Drawing chemical structures is one of the most important parts of my job. For me, although I love using LaTeX, the best tool for doing this is graphical: <a href="http://www.cambridgesoft.com">ChemDraw</a>. There are a few reasons why I favour using ChemDraw over other approaches. Most importantly of all it produces the best output I know of (although <a href="http://www.chemdoodle.com">ChemDoodle</a> is pretty close). Complex structures are hard enough to produce and edit with a graphical tool, and the challenge of using a text-based approach makes this even more tricky. Finally, it's what my colleagues use, so there is some realism involved.

On the other hand, you always need to be ready to try new approaches, so I've been meaning for a while to look at the new-ish <a href="http://ctan.org/pkg/chemfig">ChemFig</a> package, which is based on <a href="http://ctan.org/pkg/pgf">Ti<em>k</em>Z</a>. I'm starting as a lecturer next month, so with some teaching material to prepare as an incentive I've decided to take another look at ChemFig. I'm going to take two or three posts to look at how I've got on. I won't spoil the conclusions, but I think it's worth saying now that I won't be moving from ChemDraw just yet for my research work!

<h2>The target</h2>

As a first target, I decided to try to reproduce a structure I'm going to need to draw for some practical hand-outs. My favoured settings for ChemDraw are those used by the <a href="http://pubs.rsc.org/en/journals">Royal Society of Chemistry</a>, which are set up for 7 pt text to match 9 pt body text in two-column journals. I'll be coming back to these settings a bit more in the second part of this mini-series, but for the moment let's see what the result looks like:

<img class="alignnone size-medium wp-image-1910" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemDraw-300x181.png" alt="" width="300" height="181" />

The aim is to get this 'right', working out first how to get the structure correct using ChemFig, then get the finer points of the appearance right. In this post, I'll tackle the basic connectivity, and in the next one how to match the appearance.

<h2>Rings and chains</h2>

As you'd expect, the <a href="http://ctan.org/pkg/chemfig">ChemFig manual</a> covers how to produce structures in some detail. Here, I'm going to look very briefly at the syntax needed to get us started. Rather than repeat myself multiple times, I'm using a simple LaTeX document

<pre><code>\documentclass{article}
\usepackage{chemfig}
\begin{document}
% Content here
\end{document}
</code></pre>

for all of this.

The basic command we are going to need is <code>\chemfig</code>, which takes a single argument: a description of the structure required. As you might expect, this can take a bit of getting used to. For example, a benzene ring is

<pre><code>\chemfig{*6(-=-=-=)}
</code></pre>

which comes out as

<img class="alignnone size-medium wp-image-1916" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig1-260x300.png" alt="" width="260" height="300" />

The syntax here is reasonably clear: <code>*</code> makes a ring, <code>6</code> means it's a six-membered ring and <code>-=-=-=</code> is the bonding pattern in the ring.

If we just wanted a linear structure, we could omit the ring part with <code>\chemfig{-=-=-=}</code> giving

<img class="alignnone size-medium wp-image-1912" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig2-300x3.png" alt="" width="300" height="3" />

<h2>Decorating the ring</h2>

Adding substituents is not too hard once you work out that the first position on the ring is not the bottom but is the lower of the two left-hand atoms, and that the sequence runs anti-clockwise. The parenthesis in the ring part above might give you a clue that they are used to define groups inside the structure. So the left-hand ring we want is written

<pre><code>\chemfig{*6(-(-R^2)=-(-)=(-OH)-(-R^1)=)}
</code></pre>

and gives

<img class="alignnone size-medium wp-image-1913" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig3-260x300.png" alt="" width="260" height="300" />

Hopefully the pattern is reasonably clear: you need to have a <code>-</code> inside the parentheses to have the bond coming off the ring, and can use <code>^</code> for superscripts in the usual TeX way.

<h2>Completing the structure</h2>

The same scheme applies to constructing the rest of the molecule: you can put one ring as a substituent on another, and can have an atom in a chain simply by including the atom name 'in place'. However, there's a slight issue, as

<pre><code>\chemfig{
  *6(-(-R^2)=-
    (-=N-*6(=(-R^3)-=(-R^4)-=(-R^3)-))
  =(-OH)-(-R^1)=)
}
</code></pre>

is not quite right:

<img class="alignnone size-medium wp-image-1914" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig4-300x211.png" alt="" width="300" height="211" />

As you can see, the bond angle in the chain part is wrong: ChemFig does not 'auto-stagger' things. Of course, this is a pretty basic requirement, so there is a syntax to set the angle of a join: <code>[::-60]</code> will set the relative angle to 60 degrees clockwise, and all will then be well.

<pre><code>\chemfig{
  *6(-(-R^2)=-
    (-=[::-60]N-*6(=(-R^3)-=(-R^4)-=(-R^3)-))
  =(-OH)-(-R^1)=)
}
</code></pre>

<img class="alignnone size-medium wp-image-1915" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig5-300x175.png" alt="" width="300" height="175" />

That completes the connectivity we want, and as you can see the input is starting to look a bit frightening (see my comment at the start of the post). It's also not great looking compared with the ChemDraw reference version: in the next post, I'll see how that can be addressed.
