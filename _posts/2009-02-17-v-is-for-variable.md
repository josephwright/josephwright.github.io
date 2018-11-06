---
id: 184
title: V is for variable
date: 2009-02-17T08:22:46+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=184
permalink: /2009/02/17/v-is-for-variable/
categories:
  - LaTeX3
tags:
  - argument specifiers
---
There is currently a lot of activity going on with the <a title="LaTeX3 Code" href="http://www.latex-project.org/code.html">LaTeX3 code base</a>, as the team work through various issues about the code. One of the ongoing changes is to the <a title="LaTeX3 argument specifier improvements" href="http://www.texdev.net/2009/02/13/latex3-argument-specifiers-improvements/">argument specifiers</a> used in the code, where some rationalisation is taking place. Perhaps the most interesting new idea being implemented is the <code>v</code>/<code>V</code> specifier for <em>variables</em>.

The idea of the two new specifiers is that the day-to-day LaTeX programmer should not need to worry about complex runs of <code>\expandafter</code> primitives, or how variables are stored at a TeX level. LaTeX3 has some variables which are TeX primitive types (such as <code>_toks</code> or <code>_int</code>) and others which are stored as macros (<code>_tlp</code> and <code>_clist</code>, for example). Using the <code>V</code> specifier, you get the content of a variable, independent of the storage method and without needing to think about expansion. So <code>\foo:V \l_variable_type</code> is equivalent to <code>\foo:n {content of l_variable_type}</code>. We also have the <code>v</code> specifier, which first constructs a csname before getting the content: <code>\foo:v {l_variable_type}</code>.

This is quite a departure from the TeX or LaTeX2ε way of thinking about things, but makes LaTeX3 variables more more similar to those of other languages. As yet, the new specifiers have not been fully deployed in the expl3 code. However, as they are I'd expect the clarity this idea brings to be very welcome. I'm looking forward to trying it out in the experiments I've done with LaTeX3.
