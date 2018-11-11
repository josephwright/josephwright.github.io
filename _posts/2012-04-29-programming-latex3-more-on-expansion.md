---
title: Programming LaTeX3: More on expansion
layout: post
permalink: /2012/04/29/programming-latex3-more-on-expansion/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the [last post](/2012/04/21/programming-latex3-expandability/), I looked at the idea of expandability, and how we can use `x`-type expansion to exhaustively expand an argument. I also said that there was more to this, and hinted at two other argument specifications, `f`- and `o`-type expansion. We need these because TeX is a macro-expansion language, and while LaTeX3 coding does hide some of this detail it certainly does not get rid of all of it. Both of these forms of expansion are somewhat specialised, but both are also necessary!

## Full (or forced) expansion

The `f`-type ('full' or 'force') expansion argument is in some ways similar to the `x`-type concept, as it's about trying to expand as much as possible. So

```latex
\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nx \l_tmpc_tl{ \l_tmpb_tl }
\tl_show:N \l_tmpc_tl
```

and

```latex
\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nf \l_tmpc_tl{ \l_tmpb_tl }
\tl_show:N \l_tmpc_tl
```

give the same result: everything is expanded, and `\l_tmpc_tl` contains `'foo`'. There are two crucial differences, however. First, `x`-type variants are not expandable, even if their parent function was. On the other hand, `f`-type expansion is itself expandable. So something like

```latex
\cs_new:Npn \my_function:n { \tl_length:n {#1} }
\int_eval:n { \exp_args:Nf \my_function:n { \l_tmpa_tl } + 1 }
```

will work as we'd want: `\l_tmpa_tl` will be expanded, then processed by `\my_function:n` and the result will be evaluated as an integer. Try that with `\exp_args:Nx` and it will fail.

The second difference is what happens when we hit a non-expandable token. With `x`-type expansion, TeX will look at the next thing in the input, and so tries to expand _everything_ in the input (hence 'exhaustive'). On the other hand, `f`-type expansion stops when the first non-expandable token is found. So

```latex
\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { bar }
\tl_set:Nf \l_tmpc_tl { \l_tmpa_tl \l_tmpb_tl }
\tl_show:N \l_tmpc_tl
```

will show

```latex
foo\l_tmpb_tl
```

That happens because the `f` in `foo` is not expandable. So `f`-type expansion stops before it gets to `\l_tmpb_tl`, while `x`-type expansion would keep going.

The second point is important as it means that some functions will not give the expected result if used inside an `f`-type expansion. We show this in the code documentation for LaTeX3: functions which fully expand inside both `f`- and `x`-type expansions are shown with a hollow star, while those that only work inside an `x`-type expansion are shown with a filled star.

As you might pick up, `f`-type expansion is somewhat specialised. It's useful when creating expandable commands, but for non-expandable ones `x`-type expansion is usually more appropriate.

## Expanding just the once

As TeX is a macro expansion language, there are some tasks that are best carried out, or even only doable, using an exact number of expansions. To allow a single expansion, the argument specification `o` ('once') is available. To use this, you need to know what will happen after exactly one expansion. Functions which may be useful in this way have information about their expansion behaviour included in the documentation, while token list variables also expand to their content after exactly one expansion. Examples using `o`-type expansion tend to be low-level: perhaps the best example is dropping the first token from some input, so

```latex
\tl_set:No \l_tmpa_tl { \use_none:n tokens }
\tl_show:N \l_tmpa_tl
```

will show '`okens`'.

As with `f`-type expansion, expanding just once is something of a specialist tool, but one that is needed. It also completes the types of argument specification we can use, so we're now in a position to do some more serious LaTeX3 programming.
