---
id: 867
title: Local register allocation
date: 2010-12-30T18:40:26+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=867
permalink: /2010/12/30/local-register-allocation/
categories:
  - General
---
There have been a few occasions in recent weeks where the question of locally-allocated registers has come up: the most recent is here. I thought it might be useful to look at this issue: we've recently looked at this for LaTeX3 and have decided against it, at least for the moment.
<h2>TeX registers</h2>
First, a quick bit of background on variables in TeX. At the engine level, TeX provides an umber of different register types, for example counts, token registers (toks), dimensions, <em>etc</em>. These can be referred to by number, for example
<pre>\count100=123
\toks100={Tokens}</pre>
However, this would be pretty awkward with any significant number of registers. To help out, the engine provides a number of primitives to give these registers more useful names:
<pre>\countdef\mycount=100
\toksdef\mytoks=100
\mycount=123
\mytoks={Tokens}</pre>
This is clearly better, as at the point of use the register is used by name rather than by number.

There is still a need to know which number to allocate in the first place: we don't want to give the same register two (or more) names, and accidentally overwrite it. To solve this, the plain TeX format, LaTeX, <em>etc.</em>, set up an allocation system, in which the numbers already used are kept a track of. This is wrapped up inside <code>\newcount</code>, <code>\newtoks</code> and so on.
<h2>Allocating locally</h2>
Okay, how does this relate to local variables? Well, this higher-level tracking mechanism works globally, so once a register is marked as used, it never becomes available again for re-use. So if I do
<pre>\begingroup
  \newcount\mycount
  ...
\endgroup
</pre>
the register number for <code>\newcount</code> is not available at the end of the group. As there are only 256 registers of each type in Knuth's TeX, this could soon lead to a serious issue.

The <a href="http://ctan.org/pkg/etex">etex</a> package provides for both global and local allocation of registers. This means that you can do
<pre>\usepackage{etex}
\begingroup
  \loccount\mycount
  ...
\endgroup
</pre>
and have the register free up as you would expect.
<h2>What does local mean?</h2>
So does that mean that local registers are a good idea? I'd say probably not, because of what is meant here by local. In most languages, a local variable is local to some function, and nested functions have there own independent local variables. In TeX, things are different, as it is a macro language and only grouping makes things local. So something like
<!-- {% raw %} -->
<pre>\def\BadIdea{%
  \loccount\mycount
  ...
}</pre>
<!-- {% endraw %} -->
will not destroy <code>\mycount</code> at the end of the material inserted by <code>\BadIdea</code>. On the other hand, things will work within a group, so doing
<!-- {% raw %} -->
<pre>
\def\BetterIdea{%
  \begingroup
    \loccount\mycount
    ....
  \endgroup
}
</pre>
<!-- {% endraw %} -->
will destroy <code>\mycount</code> as expected.

For me, this is still not enough to mean that local allocation is a good way to work. There is always the need to track grouping, and there is not really a great gain over
<!-- {% raw %} -->
<pre>
\newcount\mycount
\def\BetterIdea{%
  \begingroup
    ....
  \endgroup
}
</pre>
<!-- {% endraw %} -->
as the TeX group is still keeping the <em>allocation</em> of <code>\mycount</code> local.

As I said at the start, we've examined this for LaTeX3, and decided that the danger of misleading people is too much to put up with, despite some gains in code clarity. So while it's an interesting area to look at, I think local allocation of registers does not really make TeX coding any easier.
