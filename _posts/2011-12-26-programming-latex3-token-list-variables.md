---
title: Programming LaTeX3: Token list variables
layout: post
permalink: /2011/12/26/programming-latex3-token-list-variables/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the [last post](/2011/12/21/programming-latex3-category-codes-tokens-and-token-lists/), I talked about the concept of a token list and some general functions which act on token lists. That's fine if you just want to take some input and 'do stuff', but a very common requirement when programming is storing input, and for that we need variables. LaTeX3 provides a number of different types of variable: we'll start with perhaps the most general of all, the _token list variable_.

## Token list variables

So what is a token list variable ('`tl`')? You might well guess from the name that its a way of storing a token list! As such, a `tl` can be used to hold just about anything, and indeed this means that several of the other variable types we'll meet later are `tl`s with a special internal structure.

Before we can save anything in a `tl`, we need to create the variable: this is a general principle of programming LaTeX3. We can then store something inside the variable by setting it:

```latex
\tl_new:N \l_mypkg_name_tl
\tl_set:Nn \l_mypkg_name_tl { Fred }
```

Hopefully, the analysis of this code is not too hard. First, `\tl_new:N` creates a new token list variable which I've called `\l_mypkg_name_tl`. (I'll explain how the naming works in a little while.) The second line will set the new `tl` to contain the text `Fred`. Assuming that the surrounding code has done nothing strange, we've stored four letter tokens in `\l_mypkg_name_tl`.

As I said, a `tl` can contain anything: we are not limited to letters. So

```latex
\tl_new:N \l_mypkg_other_tl
\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ $ ! }
```

is also perfectly-valid for the content of a token list variable (although whether we'll be able to use it safely is a different matter).

## Variable naming and TeX's grouping system

From the [earlier discussion](/2011/12/14/programming-latex3-creating-functions/) of the way that functions are named in LaTeX3, it might be obvious that there is also a system to how variables are named. Skipping over the initial `\l_`, what we've got is a module name (`mypkg`), some further description of the nature of the variable (in this case `name`), and finally the variable type (`tl`), divided up by `_` in exactly the same way we did for functions. We'll see that other variables follow the same scheme.

So what's the leading `\l_` about? This tells us about the _scope_ that we should use when setting the variable. As TeX is a macro expansion language, variables are not local to functions. However, they can be local to TeX groups, which are created in LaTeX3 using

```latex
\group_begin:
% Code here
\group_end:
```

Setting a variable locally means that any changes stay within a group

```latex
\tl_new:N \l_mypkg_name_tl
\tl_set:Nn \l_mypkg_name_tl { Fred }
\group_begin:
  \tl_set:Nn \l_mypkg_name_tl { Ginger }
\group_end:
% \l_mypkg_name_tl reverts to 'Fred'
```

On the other hand, we sometimes need _global_ variables which ignore any groups

```latex
\tl_new:N \g_mypkg_name_tl
\tl_gset:Nn \g_mypkg_name_tl { Fred }
\group_begin:
  \tl_gset:Nn \g_mypkg_name_tl { Ginger }
\group_end:
% \g_mypkg_name_tl still 'Ginger'
```

So the `\l_` or `\g_` tells you what scope the variable contents have, and whether you should `set` or `gset` it. (You can probably work out that `gset` means 'set globally'.)

## Using the content of token list variables

Okay, putting stuff into token list variables is all very well and good, but unless we can do something with the content then it's not really that useful. Of course, we can do things with the content of variables. The most basic thing to do is simply to insert the content of the `tl` into the input that TeX is working with

```latex
\tl_use:N \l_mypkg_name_tl
```

That's very handy, but we can also examine the content of a token list variable. For example, we saw before that `\tl_length:n` will produce the length of a token list, and we can do the same for a token list variable using `\tl_length:N`.

```latex
\tl_set:Nn \l_mypkg_name_tl { Fred }
\tl_length:N \l_mypkg_name_tl % '4'
```

There's a lot more we can do with token list variables, but this post is already long enough, so I'll come back to more that we can do with them in the next post.

## Tips for TeX programmers: the internals of token list variable

Experienced TeX programmers are probably wondered about token list variables, and in particular exactly what the underlying TeX structure is. A `tl` is just a macro that we are using as a variable rather than function. That should not be too much of a surprise, as storing tokens in macros is very much basic TeX programming. So `\tl_set:Nn` is almost the same as the `\def` primitive.

What might worry you slightly is that I said

```latex
\tl_new:N \l_mypkg_other_tl
\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ $ ! }
```

will work. That won't work with `\def`, and you'd normally expect to need a token register (`toks`) for this. However, we don't use `toks` for LaTeX3 programming at all, and that's because we require e-TeX. So

```latex
\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ $ ! }
```

is actually the same as

```latex
\edef \l_mypkg_other_tl { \unexpanded { \ERROR ^ _ # $ $ ! } }
```

which will allow us to put _any_ tokens inside a macro.

The other thing you might notice is that I've said that `tl`s have to be declared, even though at a TeX level this is not the case. This is a principle of good LaTeX3 programming, and although it's not enforced as standard any non-declared token list variables are coding errors. You can test for this using

```latex
\usepackage[check-declarations]{expl3}
```

which uses some slow checking code to make sure that all variables are declared before they are used.
