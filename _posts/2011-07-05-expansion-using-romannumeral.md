---
id: 1035
title: Expansion using \romannumeral
date: 2011-07-05T06:43:39+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1035
permalink: /2011/07/05/expansion-using-romannumeral/
categories:
  - General
---
There was <a href="http://tex.stackexchange.com/q/22288/73">recent question on TeX.SX about expansion</a>, where I suggested using <code>\romannumeral</code> for full expansion. This idea comes up quite often, so I thought it would be useful to look at how it works.

The <code>\romannumeral</code> primitive was intended to turn integers into roman numerals. As such, the input to <code>\romannumeral</code> should be an integer, in the same way that the input to <code>\number</code> is an integer. However, while <code>\number</code> produces output for both positive and negative integer input, <code>\romannumeral</code> produces no output at all for valid negative integer input. That is pretty clear with a simple case such as
<pre>\romannumeral -15</pre>
but becomes more powerful when used along with the <code>`</code> syntax which TeX allows for including an integer
<pre>\romannumber -`0</pre>
Here, the <code>`0</code> is converted into a integer which TeX treats as complete: <code>`0</code> is 48, but <code>`01</code> is the (terminated) integer 48 followed by a separate 1 and <em>not</em> the integer 481. The important thing for expansion, however, is that TeX always looks for an optional space to gobble after an integer, even in a case like <code>`0</code> where the integer is automatically terminated.

How does this help with expansion? It's all to do with how TeX terminate numbers. If we have the demonstration macro
<pre>\def\demo#1{%
  \detokenize\expandafter{\romannumeral-`0#1}%
}</pre>
the <code>\romannumeral</code> will produce no output (as the number it finds is -48). However, it will expand <code>#1</code> until it finds an unexpandable token. That means that something like
<pre>\def\testa{\testb}
\def\testb{\testc}
\def\testc{abc}
\demo{\testa}</pre>
will be expanded to <code>abc</code> without needing to know in advance how many expansions are needed. In a real case, this is a great way to fully-expand <code>\if...</code> tests and so on, leaving only the result, but without needing to know how many expansions are needed (and having long <code>\expandafter</code> runs).

What you should notice here is that TeX will reinsert the expanded result, and will not complain if something non-expandable appears
<pre>\def\testa{\relax}
\demo{\testa}</pre>
will print <code>\relax</code>, as this is inserted with no errors or loss of unexpandable tokens.

The only proviso here is that TeX stops at the first non-expandable item. So something like
<pre>\def\testa{ \testb}
\def\testb{123}
\demo{\testa}</pre>
will stop at the space in <code>\testa</code> and not expand <code>\testb</code>. For real applications, that is not usually an issue as we are usually aiming to expand the beginning of the input.