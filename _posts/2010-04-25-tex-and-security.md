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
Security in computer programs is always an issue, with the balance between ease of use and security never being a simple black and white line. There's a [very interesting paper](http://cseweb.ucsd.edu/~hovav/papers/csr10.html), being [presented at an upcoming conference,](http://www.usenix.org/event/leet10/tech/tech.html#Checkoway) about TeX security issues. This is particularly significant to [MiKTeX](https://www.miktex.org/) users, as it's led to a change in how MiKTeX implements certain features.

One of the well-known security questions with TeX is whether to [enable `\write18`](/2009/10/06/what-does-write18-mean/), and as a result this is off by default in [TeX Live](https://tug.org/texlive/) and MiKTeX. Another area that is of obvious concern is the `\openout` primitive, which allows writing a new file and could therefore be used for undesirable purposes. Of course, this functionality is also important: writing to files is how LaTeX manages a whole range of automated cross-referencing. So there is a balance to be struck: we need `\openout`, but not at any cost.

The TeX Live team have taken the attitude that `\openout` should be able to write within the current directory structure but not outside of it. This can be seen with a couple of very similar plain TeX test files. If you try

```latex
\newwrite\mywrite
\immediate\openout\mywrite test/test.xxx
\bye
```

then everything will be fine and the test file will be created. On the other hand

```latex
\newwrite\mywrite
\immediate\openout\mywrite ../test.xxx
\bye
```

will raise an error. The behaviour with MiKTeX was to allow both (and also absolute paths, _etc_.). That has now been altered, so that MiKTeX behaves in the same way as TeX Live (at least, that's what it looks like in my tests).

Reading the MiKTeX lists, the new behaviour is causing issues because LaTeX's `\include` relies on `\openout`. Quite a lot of MiKTeX users have been doing things like:

```latex
\include{C:/Users/&lt;user&gt;/My Documents/Chapters/chapter1.tex}
```

or

```latex
\include{../Chapters/chapter1.tex}
```

which used to work and now does not. There is a setting which enables the old behaviour, but it's not really to be recommended, I think. So users will have to rearrange their input a bit to reflect the new more secure approach.

There are some other interesting points in the paper on TeX security. One is that making a truly secure LaTeX implementation (to use as a web service) is basically impossible. The [MathTran](http://www.mathtran.org/) site gets mentioned as the most secure TeX web service: it uses a specially hardened version of plain TeX, with no access to things like `\csname`, `\catcode` and so on to make it secure. For LaTeX, that is probably not possible (at least with LaTeX2e). Worth reading, but for those of us who just use TeX on our own computers not quite so immediately relevant.
