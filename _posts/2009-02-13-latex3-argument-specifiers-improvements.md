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
One of the key ideas of <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> is argument specifiers. These are part of the name of a function which tell you both how many arguments it needs, and what happens to them. Each argument gets a single letter to describe how it is processed. One of the key things this does is make expansion much easier, as <code>\expandafter</code> runs can be avoided. It also makes it easier to have a family of similar functions which take subtly different arguments. So we might have <code>\foo:N</code>, which takes a macro name as an argument, and <code>\foo:c</code>, which creates a csname from its argument.

There have been a lot of ideas about what argument specifiers to use. This has led to a rather extended set of letters in use at the moment. The team have been reviewing them, as there are clearly too many. It looks like most of the ideas are now sorted: my personal interpretation of the plan is laid out below. The letters are best thought of in a few different “classes”, and all stand for something in English.

First, there is the <code>D</code> specifier, which means <em>do not use</em>. All of the TeX primitives are initially <code>\let</code> to a <code>D</code> name, and some are then given a second name. Only the kernel team should use anything with a <code>D</code>! Currently, there are a few primitives that you might need that have only got a <code>D</code> name in LaTeX3, but this should (hopefully) be sorted soon.

Next, there are two specifiers for <em>no manipulation </em>(pass exactly as given). For a single token, the specifier is <code>N</code>, whereas for one or more tokens in braces the specifier is <code>n</code>. Usually, if you use a single token for an <code>n</code> argument, all will be well. So for example <code>\foo:Nn \ArgumentOne {ArgumentTwo}</code> then expects to process “<code>\ArgumentOne</code>” and “<code>ArgumentTwo</code>”.

Next, and deserving a class of its own, is the <code>c</code> specifier for <em>csname</em>. A c argument will be turned into a csname before being used. So <code>\foo:c {ArgumentOne}</code> will act in the same way as<code> \foo:N \ArgumentOne</code>.

Related to <code>n</code> and <code>N</code> are the <code>v</code> and <code>V</code> specifiers, which mean <em>value of variable</em>. A variable in LaTeX3 can be a primitive TeX construct (such as a count, toks, muskip, <em>etc</em>.) or a TeX macro used to store a value (a “tlp” in LaTeX3 terminology). TeX lets us store unexpanded content in a macro using <code>\def</code>, or fully expanded using <code>\edef</code>. The <code>v</code> and <code>V</code> specifiers are used to get the content of a variable without needing to worry about how many expansions to use, which depends on whether the variable is a TeX count, a macro, a toks, <em>etc</em>. A <code>V</code> argument will be a single token (similar to <code>N</code>), so we might have <code>\foo:V \MyVariable</code>; on the other hand, using <code>v</code> a csname is constructed first, and then the value is expanded, for example <code>\foo:v {MyVariable}</code>. The key point here is that depending on the underlying nature of the variable (count, toks, macro, <em>etc</em>.) the number of expansions may vary, but at the LaTeX3 level the programmer does not need to worry about this.

There will still be places where some control of expansion is needed. Rather than need to count <code>\expandafter</code>s, LaTeX3 provides the argument specifiers <code>o</code>, <code>d</code>, <code>f</code> and <code>x</code>. Here, <code>o</code> means <em>one expansion</em>, <code>d</code> <em>double expansion</em> and <code>x</code> <em>exhaustive expansion</em> (\edef). The <code>f</code> specifier stands for <em>full expansion</em>, and in contrast to <code>x</code> stops at the first non-expandable item without trying to execute it. The difference between <code>x</code> and <code>f</code> is subtle but allows some clever expansion tricks at a low level in expl3. In all cases, the argument is expanded before passing to the underlying function. So <code>\foo:o \SomeInput</code> will expand <code>\SomeInput</code> once and pass the result to <code>\foo:n</code>, whereas <code>\foo:x \SomeInput</code> will <code>\edef</code> <code>\SomeInput</code> before sending that result to <code>\foo:n</code>. Thus expansion becomes a matter of a single letter change.

For logic tests, there are the branch specifiers <code>T</code> (<em>true</em>) and <code>F</code> (<em>false</em>). For numerical tests, there is also the <code>C</code> specifier which means <em>comparison</em>. This should be something which can be tested numerically, for example <code>{ \MyCount &gt; 10 }</code>. All three specifiers treat the input in the same way as <code>n</code> (no change), but make the logic much easier to see: <code>\foo:CTF { \MyCount &gt; 10 } { Bigger } { Not-bigger }</code>.

The letter p is used for <em>primitive TeX arguments</em> (or <em>parameters</em>). This means whatever you might put after <code>\def </code>(which is given the name <code>\def:Npn</code> in LaTeX3). This could be as simple as \<code>def:Npn \foo:N #1 { Some-code }</code>, or can even be entirely blank: <code>\def:Npn \foo: { Code-here }</code>.

Finally, there is the <code>w</code> specifier for <em>weird</em> arguments. This covers everything else, but mainly applies to delimited values (where the argument must be terminated by some arbitrary string). For example <code>\def:Npn \foo:w #1 \stop { Some-code }</code> needs to have <code>\stop</code> somewhere in the input, and is therefore weird.

There are quite a lot of letters there, but there is also a logic and it soon becomes very easy to see which one you need. All of the letters have names reflecting what they mean, so hopefully the pattern soon becomes clear.
