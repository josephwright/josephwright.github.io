---
id: 669
title: TeX and security
date: 2010-04-25T13:35:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=669
permalink: /2010/04/25/tex-and-security/
categories:
  - General
tags:
  - \write18
  - MiKTeX
  - security
  - TeX Live
---
Security in computer programs is always an issue, with the balance between ease of use and security never being a simple black and white line. There's a <a href="http://cseweb.ucsd.edu/~hovav/papers/csr10.html">very interesting paper</a>, being <a href="http://www.usenix.org/event/leet10/tech/tech.html#Checkoway">presented at an upcoming conference,</a> about TeX security issues. This is particularly significant to <a href="http://www.miktex.org/">MiKTeX</a> users, as it's led to a change in how MiKTeX implements certain features.

One of the well-known security questions with TeX is whether to <a href="http://www.texdev.net/2009/10/06/what-does-write18-mean/">enable <code>\write18</code></a>, and as a result this is off by default in <a href="http://www.tug.org/texlive/">TeX Live</a> and MiKTeX. Another area that is of obvious concern is the <code>\openout</code> primitive, which allows writing a new file and could therefore be used for undesirable purposes. Of course, this functionality is also important: writing to files is how LaTeX manages a whole range of automated cross-referencing. So there is a balance to be struck: we need <code>\openout</code>, but not at any cost.

The TeX Live team have taken the attitude that <code>\openout</code> should be able to write within the current directory structure but not outside of it. This can be seen with a couple of very similar plain TeX test files. If you try
<pre>\newwrite\mywrite
\immediate\openout\mywrite test/test.xxx
\bye</pre>
then everything will be fine and the test file will be created. On the other hand
<pre>\newwrite\mywrite
\immediate\openout\mywrite ../test.xxx
\bye
</pre>
will raise an error. The behaviour with MiKTeX was to allow both (and also absolute paths, <em>etc</em>.). That has now been altered, so that MiKTeX behaves in the same way as TeX Live (at least, that's what it looks like in my tests).

Reading the MiKTeX lists, the new behaviour is causing issues because LaTeX's <code>\include</code> relies on <code>\openout</code>. Quite a lot of MiKTeX users have been doing things like:
<pre>\include{C:/Users/&lt;user&gt;/My Documents/Chapters/chapter1.tex}</pre>
or
<pre>\include{../Chapters/chapter1.tex}
</pre>
which used to work and now does not. There is a setting which enables the old behaviour, but it's not really to be recommended, I think. So users will have to rearrange their input a bit to reflect the new more secure approach.

There are some other interesting points in the paper on TeX security. One is that making a truly secure LaTeX implementation (to use as a web service) is basically impossible. The <a href="http://www.mathtran.org/">MathTran</a> site gets mentioned as the most secure TeX web service: it uses a specially hardened version of plain TeX, with no access to things like <code>\csname</code>, <code>\catcode</code> and so on to make it secure. For LaTeX, that is probably not possible (at least with LaTeX2e). Worth reading, but for those of us who just use TeX on our own computers not quite so immediately relevant.