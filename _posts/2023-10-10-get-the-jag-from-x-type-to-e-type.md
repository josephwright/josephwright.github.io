---
title: "Get the Jag: from x-type to e-type"
layout: post
permalink: /2023/10/10/get-the-jag-from-x-type-to-e-type
categories:
  - expl3
---

## Variants

Controlling expansion has been a key part of `expl3` from day one. A basic
`expl3` function name such as `\foo:nn` shows how many unmodified braced
arguments it takes: so called `n`-type arguments. We can then create _variants_,
which can lead to expansion only once (`o`-type), to the value of a variable
(`V`-type) or to the value retrieved by constructing the name of a variable and
_then_ finding the value (`v`-type). We can do the same with single-token
(`N`-type) arguments, which are often themselves functions and can be given as a
constructed name (`c`-type).

How about exhaustively expanding _all_ of the tokens in an argument? To date,
that has been handled by `x`-type expansion. This uses `\edef`
behind-the-scenes, so the experienced TeX programmer will see that it cannot
itself work in an expansion context. Using `\edef` also has the side effect that
`#` tokens need to be doubled in the input.

## Enter `\expanded`

A little while ago now, the LaTeX Team arranged for a ['new' primitive
`\expanded` to be added to the major TeX
engines](/2018/12/06/a-new-primitive-expanded). This works almost in the same
way as `\edef` except that it is itself expandable _and_ it does not require `#`
tokens to be doubled. Using this primitive, we added `e`-type expansion to
`expl3`, and have used it for creating variants of expandable functions.

That left us with two almost-identical variants and a tricky task giving an
explanation of which to use, as there are places we want `e`-type expansion even
if the underlying function isn't expandable (where that `#` doubling business is
an issue). In particular, with a bit of care for a few edge cases, it turns out
that _everything_ that is set up for `x`-type expansion can be converted to
`e`-type. That includes things like `\cs_set_nopar:Npx`, where when you look
closely we should have called it `\cs_set_nopar:Npe` from the word go: there's
no `#` doubling as this is just `\edef` renamed.

## The pivot

So we've now made the decision to pivot toward `e`-type expansion across the
board. We'll be retaining the (now deprecated) `x`-type variants that are
already in `expl3`, but the documentation and all new variants will only be
`e`-type. Once the new release is out, package authors are encouraged to move
all of their `x`-type usage to `e`-type. The timeframe will of course depend on
the stability approach of individual package authors: for `siunitx`, I'm simply
going to step the minimum required `expl3` release and be done with it, but
others may be more cautious.

What is important here is that almost all users should see minimal impact:
provided the installed `expl3` core files match, there should be no obvious
change for end users. What we gain, though, at the code level is a lot more
consistency and clarity of design choice.

## One last variant

That leaves one additional variant: `f`-type, which is _almost_ like `e`-type
but stops at the first non-expandable token. It exists largely as we needed
something expandable before we had `e`-type, but it still has a few edge use
cases. So we won't be dropping it, but in almost all cases code using `f`-type
expansion can move to `e`-type. Again, I've done that in `siunitx` and will do a
sweep over the `expl3` core soon. So we can expect to see a move to almost no
use of `f`-type other than some specialist low-level places.

## A (more) consistent variant set

A key driver in the tidy up here is that we would like to provide as far as
possible pre-defined variants for the core `expl3` functions. That means having
some way of avoiding a combinatorial explosion: the more variants we need, the
more this is an issue. So we are aiming to get the 'core' set to `n`, `V`, `v`
and `e`, and `N` and `c`, with `o` and `f` where they are required. The latest
`expl3` release fleshes out more pre-defined variants for this set, and we
expect that to grow a little more as we try to standardise more functions around
this core set.

## Programmer action

The keen `expl3` programmer is likely wondering what they need to do in detail.
Working on the basis that you are already requiring the `expl3` release with
these changes (2023-10-10), then

- All `x`-type variants provided by `expl3` have now got a matching `e`-type, so
  you can simply change the naming unless ...
- ... you have doubled `#` tokens in an argument, in which case you also need to
  undouble them
- Replace your own `x`-type variants with `e`-type ones for internal code
- For your own documented variants, decide if you will retain, deprecate or
  remove `x`-type

As an example of the point on `#` tokens, you might currently have something like
```latex
\use:x
  {
    \cs_new:Npn \exp_not:N \mypkg_foo:w ##1 \c_colon_str ##2 \c_underscore_str
      {
        % Code using ##1 and ##2
      }
  }
```
which would need to change to 
```latex
\use:e
  {
    \cs_new:Npn \exp_not:N \mypkg_foo:w #1 \c_colon_str #2 \c_underscore_str
      {
        % Code using #1 and #2
      }
  }
```
Of course, if there are no doubled `#` to worry about, it's really just a
search-and-replace. So we can all now get on and use the 'Jag'!