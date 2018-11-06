---
id: 1278
title: 'Programming LaTeX3: Integers and integer expressions'
date: 2012-02-07T20:07:04+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1278
permalink: /2012/02/07/programming-latex3-integers-and-integer-expressions/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the [last entry](/2012/01/22/programming-latex3-more-on-token-list-variables/), I talked about token list variables. As we've seen, these can be used to hold basically anything, but at the cost that there is no internal structure. I've also hinted that LaTeX3 provides a number of richer data types. One that we will need sooner rather than later is the `int` type for storing integers. At the same time, we can look more widely at what are called _integer expression_: calculations which work with whole numbers.

## Storing integers

Based on what we have already seen with token lists, it should be no surprise that we can create and set `int` variables with function names you might be able to guess:

```latex
\int_new:N \l_my_a_int
\int_set:Nn \l_my_a_int { 1 + 1 }
\int_show:N \l_my_a_int % =&gt; '2'
```

Creating and setting the variable should seem easy enough here, but you might wonder about the result of showing the content here: it's not what we put in. That's because LaTeX3 treats the second argument of `\int_set:Nn` as an _integer expression_: something to be evaluated to give an integer.

## Integer expressions

All LaTeX3 functions which work with integers are set up to evaluate integer expressions, so it's important to understand what they do. Expressions can use the standard arithmetic operations `+`, `-`, `*` (times) and `/`, plus parentheses. There are also some functions available for additional more complicated mathematical operations (for example `\int_mod:nn` to calculate the remainder on division).

More significantly, we can include other functions which themselves yield integers. For example, we've seen that it's possible to work out the length of a token list, which is an integer:

```latex
\int_set:Nn \l_my_a_int { \tl_length:n { Hello } * 2 } % =&gt; 10
```

We can't use any function here: there are some restrictions. Clearly we need to get an integer out, but the functions also need to be _expandable_: that will be the topic of the next post!

## Integer conditionals

A key use of integers is in conditionals. [Earlier](/2011/12/21/programming-latex3-category-codes-tokens-and-token-lists/), we saw that conditionals in LaTeX3 are defined so that we have distinct `true` and `false` branches to follow. That applies to integer conditionals in exactly the same way as anything else

```latex
\int_new:N \l_my_b_int
\int_set:Nn \l_my_b_int { 7 }
\int_compare:nTF { 1 = \l_my_a_int }
  { TRUE }
  { FALSE }
\int_compare:nNnTF { \l_my_a_int } = { \l_my_b_int }
  { TRUE }
  { FALSE }
```

You might wonder what is going on here: there are two different conditionals, both of which do a comparison. Well, there are two types of integer conditionals. The first type works out where the comparator is, and so only requires three arguments. The second type has to be given the two integer expressions to compare separately. It's a bit more awkward to read, but the latter version is faster (it's closer to the underlying TeX). You can pick whichever one you prefer: as I work on low-level code, I go for speed!

Closely related to conditionals are loops, and again these come pre-defined.

```latex
\int_zero:N \l_my_a_int % Hopefully obvious!
\int_while_do:nn { \l_my_a_int &lt; 10 }
  {
    \int_use:N \l_my_a_int \\
    \int_incr:N \l_my_a_int
  }
```

Hopefully most of this code is clear: we zero the counter, then loop until it reaches 10. For each loop, I've printed (used) the value directly, then incremented it by one. (There are a whole family of these functions, with `do_while` in addition to `while_do` and `nNn` versions as for conditionals.)

## Integer expressions beyond `\int_` functions

Integer expressions are not limited to `\int_` functions. Indeed, we've [already seen one](/2011/12/14/programming-latex3-creating-functions/) in `\prg_replicate:nn`. This illustrates a general point: anywhere that LaTeX3 expects an integer, it's coded to accept integer expressions.

One function that I can't miss out here is `\int_eval:n`, which just works out the value of the expression and leaves it in the input. It underlies a lot of the higher-level use of integer expressions, and we are certain to meet it later.
