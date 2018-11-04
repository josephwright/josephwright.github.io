---
id: 1006
title: siunitx v2.2 released
date: 2011-04-14T08:24:54+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1006
permalink: /2011/04/14/siunitx-v2-2-released/
categories:
  - Packages
  - siunitx
---
As I <a href="http://www.texdev.net/2011/03/20/sorting-issues-for-consideration-for-siunitx-v2-2/">detailed a little while ago</a>, I've been working on v2.2 of <a href="http://ctan.org/pkg/siunitx">siunitx</a>. I've now released the latest version, v2.2, to <a href="http://www.ctan.org/">CTAN</a>. There are a number of small changes, introducing new features, but I thought I would highlight a few.

A long-standing feature request has been to be able to use the <a href="http://ctan.org/pkg/cancel">cancel</a> package to show how units cancel out. This is useful for teaching, although it's not of course part of the usual typesetting of units for publication. It turns out not to be too hard to allow this, so that you can now use input such as
<pre>\si[per-mode = fraction]{\cancel\kg\m\per\s\cancel\kg}</pre>
and have it come out properly. At the same time, I've made it possible to highlight particular units
<pre>\si{\highlight{green}\square\metre\candela\second}</pre>
again for teaching-related purposes.

A second long-standing request is to be able to parse uncertainties given in the form
<pre>\num{1.23 +- 0.15}</pre>
which was something more of challenge, but again is now working properly. So you can get the same output from the above and from
<pre>\num{1.23(15)}.</pre>
A final highlight is the new <code>\tablenum</code> macro. This is needed for aligning numbers inside <code>\multicolumn</code> and <code>\multirow</code>, which otherwise does not work. (At a technical level, both <code>\multicolumn</code> and <code>\mutirow</code> use the <code>\omit</code> primitive, and so the code inserted by the <code>S</code> column is not used. The <code>\tablenum</code> macro effectively makes the same approach available as a stand-alone function.)