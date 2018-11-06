---
id: 313
title: 'LaTeX3: xparse'
date: 2009-06-16T21:07:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=313
permalink: /2009/06/16/latex3-xparse/
categories:
  - LaTeX3
tags:
  - xparse
---
The next step for <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> development is to revise the two existing “xpackages” which are available to make a link between the code level and the user: xparse and template. Of the two, the xparse package is by far the easier to understand.

In LaTeX2e, you can either use the LaTeX method to create new commands:
<!-- {% raw %} -->
<pre>\newcommand*\mycommand[2][]{%
  code goes here, using #1 and #2
}</pre>
<!-- {% endraw %} -->
or you can do things yourself using a mixture of TeX primitives and LaTeX internal functions (and ignoring the issue of default value):
<!-- {% raw %} -->
<pre>\def\mycommand{%
  \@ifnextchar[{%
    \@mycommand
  }{%
    \@mycommand[]%
  }%
}
\def\@mycommand[#1]#2{%
  code goes here, using #1 and #2
}</pre>
<!-- {% endraw %} -->
This does not make for code which is easy to alter to reflect different input syntax (for example XML), or to change internal functions without knowing how the user input works. The idea of xparse is to separate out the user syntax from the internal code. Currently, exactly what tools need to be available is still being decided. The current version of xparse would expect the following syntax:
<pre>\DeclareDocumentCommand \mycommand { o m } {
  code goes here, using #1 and #2
}</pre>
The idea is that each argument is represented by a letter, for example <code>o</code> for an optional argument, <code>m</code> for a mandatory one or <code>s</code> for an optional star. This makes it possible it see immediately from the definition how many arguments are needed (one for each letter). It also means that the internal functions, which implement things, can be separated totally from the user part of the system. In that way, internal functions can have a fixed number of arguments, and leave xparse to supply them. So if the internal function needs to be changed, it does not matter how it is used, or <em>vice versa</em>.

That all sounds very good, but there are some outstanding issues. For example, handling verbatim arguments is not straight-forward. There are a couple of possible approaches to this. Either stick to a simple system, and accept that not everything can be done in the same way, or make the system more flexible but complicated. I'm currently in favour of the first approach: almost every user function is simple (especially as we have the ε-TeX extensions and so can <code>\scantokens</code> our way out of a lot of problems). I'd be interested to hear what other people think would be useful.
