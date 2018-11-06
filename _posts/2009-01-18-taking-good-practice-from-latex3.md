---
title: Taking good practice from LaTeX3
layout: post
permalink: /2009/01/18/taking-good-practice-from-latex3/
categories:
  - LaTeX3
---
[LaTeX3](https://www.latex-project.org/latex3.html) provides a well thought out low level programming environment. There is a lot the (La)TeX programmer can learn about good coding practice from the current experimental code, and I'm trying to use this in [siunitx version 2](https://github.com/josephwright/siunitx). There are lots of little points that I could highlight, but I'll pick a few out:

- Naming internal functions in a systematic way, which means longer but more logical names, such as `\si@num@out@uncert@int`, a function in siunitx 2 for processing the output of the integer part of an uncertainty in a number. Logical names make for easier to follow code.
- Using lots of small functions, rather than long ones with complex nesting.
- Adding `@aux` to a function name to show an auxiliary part of another macro, rather than some complex vowel substitution using `@`.
- Creating new functions for expansion control, rather than having `\expandafter` runs all over the place.

I'm also taking some of the other ideas in siunitx version 2. For example, where possible I'm aiming only to use `\edef` where it is really needed (unknown levels of expansion). If something needs to be expanded a known number of times, I'm going for controlled expansion instead. I've also really like the idea of switches that don't use `\iffalse` and `\iftrue` to work: much less risk of problems.
