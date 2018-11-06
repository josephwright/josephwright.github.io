---
id: 544
title: TeX counts and LaTeX counters
date: 2009-11-17T08:57:38+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=544
permalink: /2009/11/17/tex-counts-and-latex-counters/
categories:
  - General
---
When answering questions about storing and manipulating numbers, there is often a choice between using a TeX count and a LaTeX counter. For new users, the difference between the two is not necessarily clear, so I thought it would be worth summarising how things work.

At the LaTeX level, a counter is created using

```latex
\newcounter{mycounter}
```

This creates a counter initialised at zero which can then be set using

```latex
\setcounter{mycounter}{4} % Or whatever
```

or manipulated using `\stepcounter` and `\addtocounter`

```latex
\setcounter{mycounter}{0}    % Value is 0
\stepcounter{mycounter}      % Value is 1
\stepcounter{mycounter}      % Value is 2
\addtocounter{mycounter}{3}  % Value is 5
```

There are then some methods to get the counter value back out. LaTeX creates a `\the…` function for each counter, which will print the current value. In places where TeX expects a number, there is also the `\value` function:

```latex
\themycounter % Prints the current value
\ifnum\value{mycounter} &gt; \value{myothercounter}%
  % Do stuff!
\fi
```

This covers a lot of what you might want to do, so the need to use the lower-level TeX system is not obvious. Perhaps the most important thing to notice is that LaTeX's counters are set globally. That makes them good for tracking something that covers the entire document, but not as good for localised calculations.

How about at the TeX level? A count is created using

```latex
\newcount\mycount
```

where the name is a name including a backslash. Setting a count is done very simply: there is no set function

```latex
\mycount 4\relax
```

Notice the `\relax` here. Without it, TeX will continue to look for the number in the next thing it finds. This can have some odd effects, and is best avoided. Altering the value can then be carried out using `\advance`

```latex
\mycount 0\relax         % Value is 0
\advance\mycount 1\relax % Value is 1
\advance\mycount 1\relax % value is 2
\advance\mycount 3\relax % Value is 5
```

The value of a count register can be recovered using `\the` or `\number`, and the name itself can be used where TeX expects a number.

```latex
\the\mycount   % Prints the current value
\number\mycount % The same result
\ifnum\mycount &gt; \myothercount
  % Do stuff!
\fi
```

The big difference is that TeX sets count registers locally. So to do a global assignment you have to do it deliberately

```latex
\global\mycount 3\relax
```

As LaTeX is built on TeX, you might guess that LaTeX's counters are an interface to TeX's count registers, but it's not immediately obvious how this is done. The way it works is that LaTeX prefixes all of the counter names with `c@`, so that if I did

```latex
\newcount\c@mycounter
\newcounter{mycounter}
```

LaTeX would issue an error message: the counter is already defined. The other LaTeX functions then build on this, so that they manipulate the internal counters. This is all done globally and with some error checking. For example, the definition of `\addtocounter` is

<!-- {% raw %} -->
```latex
\def\addtocounter#1#2{%
  \@ifundefined{c@#1}%
    {\@nocounterr{#1}}%
    {\global\advance\csname c@#1\endcsname #2\relax}}
```
<!-- {% endraw %} -->

This checks the counter exists, and if it does globally advances it.

Why choice one or other method? Well, LaTeX does error checking and also adds some refinements (such as resetting one counter based on another). It also ensures you always include the appropriate `\relax` statements to avoid TeX picking up “extra” material for numbers. On the other hand, if you want to do local assignments then you have to use TeX's count registers: LaTeX always does global assignments.  I tend to find that for document-level things counters are best (anything I actually want to print), whereas count registers are more flexible for programming.
