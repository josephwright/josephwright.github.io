---
id: 1341
title: 'Programming LaTeX3: More on expansion'
date: 2012-04-29T12:24:03+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1341
permalink: /2012/04/29/programming-latex3-more-on-expansion/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the <a title="Programming LaTeX3: Expandability" href="http://www.texdev.net/2012/04/21/programming-latex3-expandability/">last post</a>, I looked at the idea of expandability, and how we can use <code>x</code>-type expansion to exhaustively expand an argument. I also said that there was more to this, and hinted at two other argument specifications, <code>f</code>- and <code>o</code>-type expansion. We need these because TeX is a macro-expansion language, and while LaTeX3 coding does hide some of this detail it certainly does not get rid of all of it. Both of these forms of expansion are somewhat specialised, but both are also necessary!

<h2>Full (or forced) expansion</h2>

The <code>f</code>-type (‘full’ or ‘force’) expansion argument is in some ways similar to the <code>x</code>-type concept, as it's about trying to expand as much as possible. So

<pre>\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nx \l_tmpc_tl{ \l_tmpb_tl }
\tl_show:N \l_tmpc_tl</pre>

and

<pre>\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nf \l_tmpc_tl{ \l_tmpb_tl }
\tl_show:N \l_tmpc_tl</pre>

give the same result: everything is expanded, and <code>\l_tmpc_tl</code> contains <code>‘foo</code>’. There are two crucial differences, however. First, <code>x</code>-type variants are not expandable, even if their parent function was. On the other hand, <code>f</code>-type expansion is itself expandable. So something like

<pre>\cs_new:Npn \my_function:n { \tl_length:n {#1} }
\int_eval:n { \exp_args:Nf \my_function:n { \l_tmpa_tl } + 1 }</pre>

will work as we'd want: <code>\l_tmpa_tl</code> will be expanded, then processed by <code>\my_function:n</code> and the result will be evaluated as an integer. Try that with <code>\exp_args:Nx</code> and it will fail.

The second difference is what happens when we hit a non-expandable token. With <code>x</code>-type expansion, TeX will look at the next thing in the input, and so tries to expand <em>everything</em> in the input (hence ‘exhaustive’). On the other hand, <code>f</code>-type expansion stops when the first non-expandable token is found. So

<pre>\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { bar }
\tl_set:Nf \l_tmpc_tl { \l_tmpa_tl \l_tmpb_tl }
\tl_show:N \l_tmpc_tl</pre>

will show

<pre>foo\l_tmpb_tl</pre>

That happens because the <code>f</code> in <code>foo</code> is not expandable. So <code>f</code>-type expansion stops before it gets to <code>\l_tmpb_tl</code>, while <code>x</code>-type expansion would keep going.

The second point is important as it means that some functions will not give the expected result if used inside an <code>f</code>-type expansion. We show this in the code documentation for LaTeX3: functions which fully expand inside both <code>f</code>- and <code>x</code>-type expansions are shown with a hollow star, while those that only work inside an <code>x</code>-type expansion are shown with a filled star.

As you might pick up, <code>f</code>-type expansion is somewhat specialised. It's useful when creating expandable commands, but for non-expandable ones <code>x</code>-type expansion is usually more appropriate.

<h2>Expanding just the once</h2>

As TeX is a macro expansion language, there are some tasks that are best carried out, or even only doable, using an exact number of expansions. To allow a single expansion, the argument specification <code>o</code> (‘once’) is available. To use this, you need to know what will happen after exactly one expansion. Functions which may be useful in this way have information about their expansion behaviour included in the documentation, while token list variables also expand to their content after exactly one expansion. Examples using <code>o</code>-type expansion tend to be low-level: perhaps the best example is dropping the first token from some input, so

<pre>\tl_set:No \l_tmpa_tl { \use_none:n tokens }
\tl_show:N \l_tmpa_tl</pre>

will show ‘<code>okens</code>’.

As with <code>f</code>-type expansion, expanding just once is something of a specialist tool, but one that is needed. It also completes the types of argument specification we can use, so we're now in a position to do some more serious LaTeX3 programming.