---
id: 1841
title: Making custom loaders expl3-aware
date: 2015-07-30T20:34:33+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1841
permalink: /2015/07/30/making-custom-loaders-expl3-aware/
categories:
  - LaTeX3
tags:
  - expl3
---
The <code>expl3</code> syntax used by the developing programming layer for LaTeX3 is rather different from 'traditional' TeX syntax, and therefore needs to be turned on and off using the command pair <code>\ExplSyntaxOn</code>/<code>\ExplSyntaxOff</code>. In package code making use of <code>expl3</code>, the structure

<pre><code>\ExplSyntaxOn % Or implicit from \ProvidesExplPackage
....
\usepackage{somepackage}
....
\ExplSyntaxOff % Or the end of the package
</code></pre>

will switch off <code>expl3</code> syntax for the loading of <code>somepackage</code> and so will work whether this dependency uses <code>expl3</code> or not.

This is achieved by using the LaTeX2e kernel mechanism <code>\@pushfilename</code>/<code>@popfilename</code>, which exists to deal with the status of <code>@</code> but which is extended by <code>expl3</code> to cover the new syntax too. However, this only applies as standard to code loaded using <code>\usepackage</code> (or the lower-level kernel command <code>\@onefilewithoptions</code>). Some bundles, most notable <a href="http://ctan.org/pkg/pgf">Ti<em>k</em>Z</a>, provide their own loader commands for specialised files. These can be made '<code>expl3</code>-aware' by including the necessary kernel commands

<!-- {% raw %} -->
<pre><code>\def\myloader#1{%
  \@pushfilename
  \xdef\@currname{#1}%
  % Main loader, including \input or similar
  \@popfilename
}
</code></pre>
<!-- {% endraw %} -->

For packages which also work with formats other than LaTeX, the push and pop steps can be set up using <code>\csname</code>

<!-- {% raw %} -->
<pre><code>\def\myloader#1{%
  \csname @pushfilename\endcsname
  \expandafter\xdef\csname @currname\endcsname{#1}%
  % Main loader, including \input or similar
  \csname @popfilename\endcsname
}
</code></pre>
<!-- {% endraw %} -->

Of course, that will only work with LaTeX (the stack is not present in plain TeX or ConTeXt), but as the entire package idea is essentially a LaTeX one that should be a small problem.
