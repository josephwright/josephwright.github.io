---
id: 171
title: LaTeX3 argument specifiers improvements
date: 2009-02-13T08:28:35+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=171
permalink: /2009/02/13/latex3-argument-specifiers-improvements/
categories:
  - LaTeX3
tags:
  - argument specifiers
---
One of the key ideas of [LaTeX3](http://www.latex-project.org/latex3.html) is argument specifiers. These are part of the name of a function which tell you both how many arguments it needs, and what happens to them. Each argument gets a single letter to describe how it is processed. One of the key things this does is make expansion much easier, as `\expandafter` runs can be avoided. It also makes it easier to have a family of similar functions which take subtly different arguments. So we might have `\foo:N`, which takes a macro name as an argument, and `\foo:c`, which creates a csname from its argument.

There have been a lot of ideas about what argument specifiers to use. This has led to a rather extended set of letters in use at the moment. The team have been reviewing them, as there are clearly too many. It looks like most of the ideas are now sorted: my personal interpretation of the plan is laid out below. The letters are best thought of in a few different “classes”, and all stand for something in English.

First, there is the `D` specifier, which means _do not use_. All of the TeX primitives are initially `\let` to a `D` name, and some are then given a second name. Only the kernel team should use anything with a `D`! Currently, there are a few primitives that you might need that have only got a `D` name in LaTeX3, but this should (hopefully) be sorted soon.

Next, there are two specifiers for _no manipulation_ (pass exactly as given). For a single token, the specifier is `N`, whereas for one or more tokens in braces the specifier is `n`. Usually, if you use a single token for an `n` argument, all will be well. So for example `\foo:Nn \ArgumentOne {ArgumentTwo}` then expects to process “`\ArgumentOne`” and “`ArgumentTwo`”.

Next, and deserving a class of its own, is the `c` specifier for _csname_. A c argument will be turned into a csname before being used. So `\foo:c {ArgumentOne}` will act in the same way as` \foo:N \ArgumentOne`.

Related to `n` and `N` are the `v` and `V` specifiers, which mean _value of variable_. A variable in LaTeX3 can be a primitive TeX construct (such as a count, toks, muskip, _etc_.) or a TeX macro used to store a value (a “tlp” in LaTeX3 terminology). TeX lets us store unexpanded content in a macro using `\def`, or fully expanded using `\edef`. The `v` and `V` specifiers are used to get the content of a variable without needing to worry about how many expansions to use, which depends on whether the variable is a TeX count, a macro, a toks, _etc_. A `V` argument will be a single token (similar to `N`), so we might have `\foo:V \MyVariable`; on the other hand, using `v` a csname is constructed first, and then the value is expanded, for example `\foo:v {MyVariable}`. The key point here is that depending on the underlying nature of the variable (count, toks, macro, _etc_.) the number of expansions may vary, but at the LaTeX3 level the programmer does not need to worry about this.

There will still be places where some control of expansion is needed. Rather than need to count `\expandafter`s, LaTeX3 provides the argument specifiers `o`, `d`, `f` and `x`. Here, `o` means _one expansion_, `d` _double expansion_ and `x` _exhaustive expansion_ (\edef). The `f` specifier stands for _full expansion_, and in contrast to `x` stops at the first non-expandable item without trying to execute it. The difference between `x` and `f` is subtle but allows some clever expansion tricks at a low level in expl3. In all cases, the argument is expanded before passing to the underlying function. So `\foo:o \SomeInput` will expand `\SomeInput` once and pass the result to `\foo:n`, whereas `\foo:x \SomeInput` will `\edef` `\SomeInput` before sending that result to `\foo:n`. Thus expansion becomes a matter of a single letter change.

For logic tests, there are the branch specifiers `T` (_true_) and `F` (_false_). For numerical tests, there is also the `C` specifier which means _comparison_. This should be something which can be tested numerically, for example `{ \MyCount &gt; 10 }`. All three specifiers treat the input in the same way as `n` (no change), but make the logic much easier to see: `\foo:CTF { \MyCount &gt; 10 } { Bigger } { Not-bigger }`.

The letter p is used for _primitive TeX arguments_ (or _parameters_). This means whatever you might put after `\def` (which is given the name `\def:Npn` in LaTeX3). This could be as simple as `\def:Npn \foo:N #1 { Some-code }`, or can even be entirely blank: `\def:Npn \foo: { Code-here }`.

Finally, there is the `w` specifier for _weird_ arguments. This covers everything else, but mainly applies to delimited values (where the argument must be terminated by some arbitrary string). For example `\def:Npn \foo:w #1 \stop { Some-code }` needs to have `\stop` somewhere in the input, and is therefore weird.

There are quite a lot of letters there, but there is also a logic and it soon becomes very easy to see which one you need. All of the letters have names reflecting what they mean, so hopefully the pattern soon becomes clear.
