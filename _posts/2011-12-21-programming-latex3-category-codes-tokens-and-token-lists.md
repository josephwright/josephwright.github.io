---
title: "Programming LaTeX3: Category codes, tokens and token lists"
layout: post
permalink: /2011/12/21/programming-latex3-category-codes-tokens-and-token-lists/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
Understanding LaTeX3 programming relies on understanding TeX concepts, and one we need to get to grips with is how TeX deals with tokens. Experienced TeX programmers will probably find the first part of this post very straight-forward, so might want to skim read the start!

## Category codes and tokens

When TeX reads input, it is not only the characters that are there that are important. Each character has an associated _category code_: a way to interpret that character. The combination of a character and it's category code then sets how TeX will deal with the input. For example, when TeX read '`a`' it finds that it's (normally) a letter, and so tokenizes the input as '`a`, `letter`'. This seems pretty obvious: 'a' _is_ a letter, after all. But this is not fixed, at least for TeX. I've already mentioned that within the LaTeX3 programming environment `:` and `_` can be part of function names: that's because they are 'letters' while we are programming! What's of most importance now is that a control sequence (something like `\emph` or `\cs_new:Npn`) is stored as a single token. So most of the time it these can't be divided up into their component characters: they act as a single item.

## Token lists

The fact that TeX works with tokens means that most of the time we carry out operations on a token-by-token basis, rather than as strings. In LaTeX3  terminology, an arbitrary set of tokens is called a _token list_, and which of has both defined content and defined order. To get a better feel for how token lists work, we'll apply a few basic token list functions to some simple input:

```latex
\documentclass{article}
\usepackage{expl3}
\ExplSyntaxOn
\cs_new:Npn \demo:n #1
  {
    \tl_count:n {#1} ;
    \tl_if_empty:nT {#1} { Empty! }
    \tl_if_blank:nTF {#1}
      { Blank! }
      {
        Head = \tl_head:n {#1} ;
        Tail = \tl_tail:n {#1} ;
        End
      }
  }
\cs_new_eq:NN \demo \demo:n
\ExplSyntaxOff
\newcommand*{\hello}{hello}
\begin{document}
\demo{Hello world}

\demo{ }

\demo{}

\demo{\hello}
\end{document}
```

Okay, what's going on here? Well, as we saw

[last time](/2011/12/14/programming-latex3-creating-functions/) I've created a new function, in this case called `\demo:n`, which contains the code I want to use. In contrast to the last post, I've not used it directly but have instead used `\cs_new_eq:NN` to make a copy of this function but with a document-level name. This is a general LaTeX3 idea: the internals of your code should be defined separately from the interface (indeed, we'll see later that there is a more formalised way of creating a document-level function). You can probably work out that `\cs_new_eq:NN` needs two arguments: the new function to create and the old one to copy. (For experienced TeX programmers, it will be no surprise that this is a wrapper around the `\let` primitive.) Moving on to what `\demo:n` is doing, the first thing to see is that I've defined it with one argument, agreeing with the `:n` part of its name. I've then done some simple tests on the argument. The first is `\tl_count:n`, which will count how many tokens are in the input and simply output the result. You'll notice that it's ignored the space in `Hello world`: it's a common feature of TeX that spaces are often skipped over. You can also see the space-skipping behaviour in the line where I feed `\demo` a space: the result has a 'length' of zero. Also notice that as promised `\hello` is only a single token. (There is an experimental function in LaTeX3 to count the length of a token list _including_ the spaces. Most of the time, we'll actually want to ignore them so we won't worry about that here!) We then have to _conditionals_, `\tl_if_empty:nT` and `\tl_if_blank:nTF`. First, we'll look at what a conditional does in general, then at these two in particular. The LaTeX3 approach to conditionals is to accept either one or two arguments, which might read `T`, `F` or `TF`, so in general there are always three related functions:

```latex
\foo_if_something:nT
\foo_if_something:nF
\foo_if_something:nTF
```

The test is always the same for the three related versions, with the

`T` and `F` part tells us what code is used depending on the result of the test. So if we do a test and it's true, the `T` code will be used if it's there, and the `F` code will be skipped entirely, while if there is no `T` code then nothing happens. It's of course the other way around when the test is false! So what's happening with `\tl_if_empty:nT` and `\tl_if_blank:nTF`? In the first test, we only print `{ Empty! }` if there is nothing _at all_ in the argument to `\demo:n`. If the argument is no empty, then this test does nothing at all. On the other hand, the `\tl_if_blank:nTF` test will print `{ Blank! }` if the argument is either entirely empty or is only made up of spaces (so it looks blank). However, if it's not blank then we apply two more functions. The functions `\tl_head:n` and `\tl_tail:n` find the very first token and everything but the very first token, respectively. So `\tl_head:n` finds just the `H` of `Hello world` while `\tl_tail:n` finds `ello world`. I've only used them if the entire argument is not blank as they are not really designed to deal with cases where there is nothing to split up! You might wonder about the last test, where `\demo{\hello}` has `Hello` as the head part and nothing as the tail. That happens because what is tested here is `\hello`, a single token, which is then turned into the text we see by TeX during typesetting. That can be avoided, but at this stage we'll not worry too much!
