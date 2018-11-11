---
title: Programming LaTeX3: Expandability
layout: post
permalink: /2012/04/21/programming-latex3-expandability/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the [last part](/2012/02/07/programming-latex3-integers-and-integer-expressions/), I looked at integer expressions, and how they can be used to calculate integer values. What I did not do was say exactly what can go inside an integer expression. That's because it links in to a wider concept, and one that is very familiar to TeX programmers: expandability.

## What is expandability?

To understand expandability, we need to think about what TeX does when we use functions. TeX is a macro expansion language, and as I've already said that means that LaTeX3 is too. When we use a function in a place where TeX can execute all of the built-in commands ('primitives'), we don't really need to worry about that too much. However, there are places where life is more complicated, as TeX will only execute some of the primitives. These places are 'expansion contexts'. In these places, only some functions will work as expected, and so it's important to know what will and will not work.

## LaTeX3 and expandability

For traditional TeX programmers, understanding expandability means knowing the rules that TeX applies to decide what can and cannot be expanded. For LaTeX3, life is different as the documentation includes details of what will and will not work. If you read the documentation, you will see that some functions are marked with a star: those are expandable. For the moment, we won't worry about the non-starred functions, other than to note that we can't use them when we need expandability.

So sticking with our starting point, integer expressions, if we look at a function like `\int_eval:n`, this leads to the conclusion that the argument can only contain

- Numbers, either given directly or stored inside variables
- The symbols `+`, `-`, `*`, `\`, `(` and `)`
- Functions which are marked with a star in the LaTeX3 documentation, plus any arguments these themselves need.

That hopefully makes some sense: `\int_eval:n` is supposed to produce a number, and so what we put in should make sense for turning into a number. The same idea applies to all of the other integer expression functions we saw last time.

## Expansion in our own functions

Integer expression functions make a good example for expandability, but if that was the only area that expansion applied it would not be that significant. However, there are lots of other places where we want to carry out expansion, and this takes us back to the idea of the argument specification for functions. There are three expansion related argument specifiers: `f`, `o` and `x`. Here, I'm going to deal just with `x`-type expansion, and will talk about `f`- and `o`-type expansion next time!

So what is `x`-type expansion? It's exhaustive: expanding everything until only non-expandable content remains. We've [already seen](/2012/01/22/programming-latex3-more-on-token-list-variables/) the idea that for example `\tl_put_right:NV` is related to `\tl_put_right:Nn`, so that we can access the value of a variable. So it should not be too much of a leap to see a relationship between `\tl_set:Nn` and `\tl_set:Nx`. So when we do

```latex
\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nx \l_tmpc_tl { \l_tmpb_tl }
\tl_show:N \l_tmpc_tl
```

TeX exhaustively expands: it expands `\l_tmpb_tl`, and finds `\l_tmpa_tl`, then expands `\l_tmpa_tl` to `foo`, then stops as letters are not expandable. Inside an `x`-type expansion, TeX just keeps going! So we don't need to know much about the _content_ we are expanding.

With a function such as `\int_eval:n`, the argument specification is just `n`, so you might wonder why. The reason is that `x`-type functions are (almost) always defined as a variant of an `n`-type parents. So functions that have to expand material (there is no choice) just have an `n`. (There are also a few things that `\int_eval:n` will expand that and `x`-type argument will not, but in general that's not an issue as it only shows up if you make a mistake.)

## Functions that can be expanded

I've said that functions that can be expanded fully are marked with a star in the documentation, but how do you make your own functions that can be expanded? It's not too complicated: a function is expandable if it uses only expandable functions. So if all of the functions you use are marked with a star, then yours would be too.

There is a bit more to this, though. We have two (common) ways of creating new functions

- `\cs_new:Npn`
- `\cs_new_protected:Npn`

The difference is expandability. Protected functions are not expandable, whereas ones created with `\cs_new:Npn` should be. So the rule is to use `\cs_new_protected:Npn` _unless_ you are sure that your function is expandable.

## LaTeX2e hackers note: What about `\protected@edef`?

Experienced TeX hackers will recognise that `x`-type expansion is build around TeX's `\edef` primitive. If you've worked a lot with LaTeX2e, you'll know that with any user input you should use `\protected@edef`, rather than `\edef`, so that LaTeX2e robust commands are handled safely.

If you are working with LaTeX2e input, you'll still need to use `\protected@edef` to be safe when expanding arbitrary user input. All LaTeX3 functions are either fully-expandable or engine-protected, so don't need the LaTeX2e mechanism, but of course that is not true for LaTeX2e commands.
