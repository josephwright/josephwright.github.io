---
title: V is for variable
layout: post
permalink: /2009/02/17/v-is-for-variable/
categories:
  - LaTeX3
tags:
  - argument specifiers
---
There is currently a lot of activity going on with the [LaTeX3 code base](https://www.latex-project.org/code.html), as the team work through various issues about the code. One of the ongoing changes is to the [argument specifiers](/2009/02/13/latex3-argument-specifiers-improvements/) used in the code, where some rationalisation is taking place. Perhaps the most interesting new idea being implemented is the `v`/`V` specifier for _variables_.

The idea of the two new specifiers is that the day-to-day LaTeX programmer should not need to worry about complex runs of `\expandafter` primitives, or how variables are stored at a TeX level. LaTeX3 has some variables which are TeX primitive types (such as `_toks` or `_int`) and others which are stored as macros (`_tlp` and `_clist`, for example). Using the `V` specifier, you get the content of a variable, independent of the storage method and without needing to think about expansion. So `\foo:V \l_variable_type` is equivalent to `\foo:n {content of l_variable_type}`. We also have the `v` specifier, which first constructs a csname before getting the content: `\foo:v {l_variable_type}`.

This is quite a departure from the TeX or LaTeX2e way of thinking about things, but makes LaTeX3 variables more similar to those of other languages. As yet, the new specifiers have not been fully deployed in the `expl3` code. However, as they are I'd expect the clarity this idea brings to be very welcome. I'm looking forward to trying it out in the experiments I've done with LaTeX3.
