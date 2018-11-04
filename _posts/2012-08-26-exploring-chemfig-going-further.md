---
id: 1529
title: 'Exploring ChemFig: Going further'
date: 2012-08-26T09:07:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1529
permalink: /2012/08/26/exploring-chemfig-going-further/
categories:
  - General
tags:
  - ChemFig
  - chemistry
  - tikz
---
In the first two parts of this short series, I've looked at some <a href="http://www.texdev.net/2012/08/25/exploring-chemfig-basics/">ChemFig basics</a> and <a href="http://www.texdev.net/2012/08/25/exploring-chemfig-customising-appearance/">improving the settings used to get to publication-quality appearance</a>. In this final part, I want to look as some more complex effects. I'm going to keep using the customisations I made in part two, so the demos here all use them in the preamble.

<h2>Decorating bonds</h2>

Chemists don't only use simple line bonds: we use bold, dashed and wavy lines a lot. ChemDraw has all of these set up 'out of the box':

<img class="alignnone size-full wp-image-1926" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemDraw2.png" alt="" width="196" height="125" />

ChemFig does not have a simple input syntax for them, unlike <code>=</code> for a double bond or <code>~</code> for a triple bond. However, it does let us customise bond appearance: the basic syntax we need is to put <code>[,,,,&lt;settings&gt;]</code> after the bond to be customised (there are four commas here as ChemFig has other settings to alter bonding). The settings are Ti<i>k</i>Z commands, and it's possible to set up these customisations as styles, which is better than doing everything by hand.

First, we need two settings from ChemDraw: the thickness to use for a bold bond and the spacing in a hashes. I'll want to use these a few times, so save them with readable names

<pre><code>\newcommand*{\bondboldwidth}{0.22832 em} %'Bold Width'
\newcommand*{\bondhashlength}{0.25737 em} % 'Hash Spacing'
</code></pre>

Bold, hashed and dashed bonds are then easy to set up

<pre><code>\tikzset{
  bold bond/.style = {line width = \bondboldwidth},
  dash bond/.style =
    {dash pattern = on \bondhashlength off \bondhashlength},
  hash bond/.style =
    {
      dash pattern = on \bondwidth off \bondhashlength,
      line width   = \bondboldwidth
    },
}
</code></pre>

Wavy bonds are a bit more tricky. Ti<i>k</i>Z has a 'decorations' library including the idea of a 'snake' line, but this is not quite right. Instead, I'll use a 'real' sine wavy as <a href="http://tex.stackexchange.com/a/25689/73">described on the TeX-sx site</a>.
At the same time, I want to pick up something 'internal' from ChemFig: the inter-atom spacing, which we set using <code>\setatomsep</code>. That's stored in the macro <code>CF@atom@sep</code>, which I want as wavy bonds should have an integer number of repetitions along a standard-length bond:

<pre><code>\tikzset{
  wavy bond/.style =
    {
      decorate,
      decoration =
        {
          complete sines,
          amplitude   = \bondboldwidth,
          post length = 0 pt,
          pre length  = 0 pt,
          % Use the atom spacing: saved 
          segment length = 
            \the\dimexpr\csname CF@atom@sep\endcsname/5\relax
        }
    }
}
</code></pre>

Okay, so how does this all look? The document input is not so bad

<pre><code>\chemfig{
  *6((-[,,,,hash bond])-
  -(-[,,,,wavy bond])
  -(-[,,,,dash bond])-
  -(-[,,,,bold bond])-)
}
</code></pre>

and gives result

<img class="alignnone size-full wp-image-1924" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig10.png" alt="" width="262" height="157" />

If you look really carefully, you'll see that this highlights an issue. The bond junctions are just flat 'ends', which does not show very much for the single bonds but does where the bold bond meets the ring. If you compare with ChemDraw, you'll see that it does not make the same error: the bonds 'run in' to each other. I've not found a way to solve that, unfortunately.

<h2>Into three dimensions</h2>

Chemical structures exist in three dimensions, and it's very common to show this using wedged bonds, invented by Cram.

<img class="alignnone size-full wp-image-1927" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemDraw3.png" alt="" width="199" height="221" />

ChemFig let's us use <code>&lt;</code> in place of <code>-</code> for a filled wedged bond, with <code>&lt;|</code> for a hollow one and <code>&lt;:</code> for a dashed (backward) one. So the input we want here is

<pre><code>\chemfig{
  *6((&lt;)-(&lt;:)-(&lt;|)-(&gt;)-(&gt;:)-(&gt;|)-)
}
</code></pre>

If you try that with no setting changes, the bonds are too wide at the ends. That's controlled by <code>\setcrambond</code>, which has three parameters: the width of the bond, the thickness of hash lines and the hash line spacings. ChemDraw seems to set the wider end to the width of a bold bond plus two normal bonds, so I used

<pre><code>\setcrambond
  {\the\dimexpr \bondwidth * 2 + \bondboldwidth \relax}
  {\bondwidth}{\bondhashlength}
</code></pre>

and got

<img class="alignnone size-full wp-image-1929" src="https://www.texdev.net/wp-content/uploads/2012/08/ChemFig12.png" alt="" width="266" height="296" />

Here, it's clear that the issue with bond joins shows up a lot more than the earlier cases: it's still reasonably subtle, but definitely shows up more strongly.

<h2>Schemes and so on</h2>

I'm focussing here on drawing individual structures, but should mention schemes and compound numbering. In the MyChemistry article I've already linked to, there is quite a bit about this, using a combination of ChemFig (for the schemes) and <a href="http://ctan.org/pkg/chemnum"><code>chemnum</code></a> for the numbering. What I will say is that it works well provided you don't have complex alignment needs: one of the tricky parts of creating a good-looking scheme is deciding exactly what to line up!

The other quick note I'd add on schemes is that the arrow width really should match that of bonds. So I'd use

<pre><code>\setarrowdefault{,,line width = \bondwidth}
</code></pre>

in my preamble to have everything match.

<h2>Conclusions</h2>

With a bit of effort with the settings, ChemFig can produce quality output, and can get quite a bit 'right' (although there are a few gaps). However, as I said in the <a href="http://www.texdev.net/2012/08/25/exploring-chemfig-basics/">first part</a>, I won't be abandoning <a href="http://www.cambridgesoft.com/">ChemDraw</a> any time soon. I deliberately picked something reasonably straight-forward for my tests, and the sort of thing I do in my research work would be a <em>lot</em> harder to draw and maintain using ChemFig. In particular, I don't fancy trying to show up three-dimensional affects (for example a benzene ring going 'into' the page) using a text-based approach.

So what could I recommend ChemFig for? First, the most obvious case is for people who don't have a copy of ChemDraw. There are other graphical editors, but none of the free ones are as good as ChemDraw. So if you want high-quality output without paying, this looks the best approach I've seen. It also looks good for creating stand-alone documents (using ChemDraw means needing graphics files). That does look useful for me for teaching, where the structures will be in general not so complicated and where it will be perhaps better to have only a single <code>.tex</code> file. There's also the fact that drawing using Ti<i>k</i>Z means that the font match using ChemFig is exact: no need to try to measure up different fonts by eye. So there are uses for ChemFig, and it's certainly an interesting package. Now all we need is someone to write a ChemDraw to ChemFig converter!