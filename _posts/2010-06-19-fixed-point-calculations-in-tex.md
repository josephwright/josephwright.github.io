---
id: 748
title: Fixed point calculations in TeX
date: 2010-06-19T14:20:28+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=748
permalink: /2010/06/19/fixed-point-calculations-in-tex/
categories:
  - LaTeX3
tags:
  - fixed point
  - floating point
---
It's well-known that TeX is good at integer arithmetic, and does not provide any primitive functions for real number calculations. Experienced TeX programmers will know that you can make use of dimen registers to do real number calculations at speed, at the cost of accuracy (as TeX truncates dimensions at five decimal places). However, this is not exactly ideal and can be a bit awkward to use.

An alternative for LaTeX users is to use the<a title="Fixed point arithmetic" href="http://ctan.org/pkg/fp"> fp</a> package (which has been around since LaTeX 2.09). This is a powerful package, but can be rather slow. Part of the reason is that it allows 18 digits either side of the decimal point: a wide range of numbers, but almost certainly overkill in most cases. For applications that really need large numbers (such as <a title="Create normal/logarithmic plots in two and three dimensions" href="http://ctan.org/pkg/pgfplots">pgfplots</a>) input using floating points (such as <code>1.23e20</code>) is probably better. Floating point calculations make life a bit more complex again, but can be done in TeX (see for example <a title="Create PostScript and PDF graphics in TeX" href="http://ctan.org/pkg/pgf">pgfmath</a>).

For <a title="LaTeX3 Project" href="http://www.latex-project.org/latex3.html">LaTeX3</a> I've been working on what would be a sensible approach: real number functions are needed in various places. At the moment, the plan is to support fixed-point numbers with nine digits either side of the decimal place, so up to 999999999.999999999. That should be enough for most application, and at some stage supporting floating-point numbers might well be added. To date there is only basic arithmetic (add, subtract, multiply an divide) in the new code, but the plan is to add trigonometric and logarithmic functions. I'm sure that there will be other functions to add: I'll be interested to see what is asked for.

One area that I've been working is overall performance compared to the fp package. The biggest single gain is of course moving from 18 plus 18 digits to 9 plus 9, which makes quite a big difference on it's own. However, there are various places inside the code where there are opportunities to save time. First, as LaTeX3 requires ε-TeX I've exploited the <code>\numexpr</code> primitive where it makes a difference (mainly where it cuts down on the number of assignments needed). At the same time, there are places where using delimited macros is faster than actually doing mathematics! The exact performance gains depend on what exactly you are doing, but it is possible to draw some comparisons. Doing lots of repeated calculations it's possible to get some feel for the difference between fp and the new LaTeX3 module. On my system 100 000 additions take 31.6 s with fp and 6.0 s with l3fp, while for 20 000 divisions it takes 64.8 s with fp and 4.1 s using l3fp. Quite some speed enhancement, and I think enough to justify using the new code!
