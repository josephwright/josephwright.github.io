---
id: 1302
title: 'Programming LaTeX3: Expandability'
date: 2012-04-21T20:02:58+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1302
permalink: /2012/04/21/programming-latex3-expandability/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the <a title="Programming LaTeX3: Integers and integer expressions" href="http://www.texdev.net/2012/02/07/programming-latex3-integers-and-integer-expressions/">last part</a>, I looked at integer expressions, and how they can be used to calculate integer values. What I did not do was say exactly what can go inside an integer expression. That's because it links in to a wider concept, and one that is very familiar to TeX programmers: expandability.

<h2>What is expandability?</h2>

To understand expandability, we need to think about what TeX does when we use functions. TeX is a macro expansion language, and as I've already said that means that LaTeX3 is too. When we use a function in a place where TeX can execute all of the built-in commands (‘primitives’), we don't really need to worry about that too much. However, there are places where life is more complicated, as TeX will only execute some of the primitives. These places are ‘expansion contexts’. In these places, only some functions will work as expected, and so it's important to know what will and will not work.

<h2>LaTeX3 and expandability</h2>

For traditional TeX programmers, understanding expandability means knowing the rules that TeX applies to decide what can and cannot be expanded. For LaTeX3, life is different as the documentation includes details of what will and will not work. If you read the documentation, you will see that some functions are marked with a star: those are expandable. For the moment, we won't worry about the non-starred functions, other than to note that we can't use them when we need expandability.

So sticking with our starting point, integer expressions, if we look at a function like <code>\int_eval:n</code>, this leads to the conclusion that the argument can only contain

<ul>
    <li>Numbers, either given directly or stored inside variables</li>
    <li>The symbols <code>+</code>, <code>-</code>, <code>*</code>, <code>\</code>, <code>(</code> and <code>)</code></li>
    <li>Functions which are marked with a star in the LaTeX3 documentation, plus any arguments these themselves need.</li>
</ul>

That hopefully makes some sense: <code>\int_eval:n</code> is supposed to produce a number, and so what we put in should make sense for turning into a number. The same idea applies to all of the other integer expression functions we saw last time.

<h2>Expansion in our own functions</h2>

Integer expression functions make a good example for expandability, but if that was the only area that expansion applied it would not be that significant. However, there are lots of other places where we want to carry out expansion, and this takes us back to the idea of the argument specification for functions. There are three expansion related argument specifiers: <code>f</code>, <code>o</code> and <code>x</code>. Here, I'm going to deal just with <code>x</code>-type expansion, and will talk about <code>f</code>- and <code>o</code>-type expansion next time!

So what is <code>x</code>-type expansion? It's exhaustive: expanding everything until only non-expandable content remains. We've <a title="Programming LaTeX3: More on token list variables" href="http://www.texdev.net/2012/01/22/programming-latex3-more-on-token-list-variables/">already seen</a> the idea that for example <code>\tl_put_right:NV</code> is related to <code>\tl_put_right:Nn</code>, so that we can access the value of a variable. So it should not be too much of a leap to see a relationship between <code>\tl_set:Nn</code> and <code>\tl_set:Nx</code>. So when we do

<pre>\tl_set:Nn \l_tmpa_tl { foo }
\tl_set:Nn \l_tmpb_tl { \l_tmpa_tl }
\tl_set:Nx \l_tmpc_tl { \l_tmpb_tl }
\tl_show:N \l_tmpc_tl</pre>

TeX exhaustively expands: it expands <code>\l_tmpb_tl</code>, and finds <code>\l_tmpa_tl</code>, then expands <code>\l_tmpa_tl</code> to <code>foo</code>, then stops as letters are not expandable. Inside an <code>x</code>-type expansion, TeX just keeps going! So we don't need to know much about the <em>content</em> we are expanding.

With a function such as <code>\int_eval:n</code>, the argument specification is just <code>n</code>, so you might wonder why. The reason is that <code>x</code>-type functions are (almost) always defined as a variant of an <code>n</code>-type parents. So functions that have to expand material (there is no choice) just have an <code>n</code>. (There are also a few things that <code>\int_eval:n</code> will expand that and <code>x</code>-type argument will not, but in general that's not an issue as it only shows up if you make a mistake.)

<h2>Functions that can be expanded</h2>

I've said that functions that can be expanded fully are marked with a star in the documentation, but how do you make your own functions that can be expanded? It's not too complicated: a function is expandable if it uses only expandable functions. So if all of the functions you use are marked with a star, then yours would be too.

There is a bit more to this, though. We have two (common) ways of creating new functions

<ul>
    <li><code>\cs_new:Npn</code></li>
    <li><code>\cs_new_protected:Npn</code></li>
</ul>

The difference is expandability. Protected functions are not expandable, whereas ones created with <code>\cs_new:Npn</code> should be. So the rule is to use <code>\cs_new_protected:Npn</code> <em>unless</em> you are sure that your function is expandable.

<h2>LaTeX2e hackers note: What about <code>\protected@edef</code>?</h2>

Experienced TeX hackers will recognise that <code>x</code>-type expansion is build around TeX's <code>\edef</code> primitive. If you've worked a lot with LaTeX2e, you'll know that with any user input you should use <code>\protected@edef</code>, rather than <code>\edef</code>, so that LaTeX2e robust commands are handled safely.

If you are working with LaTeX2e input, you'll still need to use <code>\protected@edef</code> to be safe when expanding arbitrary user input. All LaTeX3 functions are either fully-expandable or engine-protected, so don't need the LaTeX2e mechanism, but of course that is not true for LaTeX2e commands.
