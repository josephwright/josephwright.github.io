---
id: 361
title: Speed versus clarity
date: 2009-07-28T19:41:52+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=361
permalink: /2009/07/28/speed-versus-clarity/
categories:
  - LaTeX3
  - Packages
  - siunitx
---
Programming complex functions in TeX tends to involve a lot of manipulation of variables. At the low level, TeX doesn't provide a lot of variable types, and so most things are done using macros. This means that a lot of array or record-type work is done by using large numbers of macros and giving them appropriate names. This is fast, as there is no need to recover data from a larger structure, but doesn't make for easy to read code.

One aim of [LaTeX3](https://www.latex-project.org/latex3.html) is to provide better programming tools built on TeX, and this includes higher-level variable support. If you take a look at the [expl3 manual](http://mirror.ctan.org/macros/latex/contrib/l3kernel/expl3.pdf), you'll find that there is support for ideas such as property lists an sequence stacks. These are, of course, implemented using macro or token registers, but provide some of the more abstract ideas that other programming languages provide for variables. The pay-off is in speed: there will always be a cost to adding layers on top of the TeX basics.

I've been worrying about how to use the new structures as I work on [siunitx version 2](https://github.com/josephwright/siunitx). My original code uses lots of macros to store things, but the result is that the code is difficult to read and even harder to change. My earlier attempts at improving the code stuck with this approach, but rationalised it into something more systematic. Better than version 1, but I've not been entirely happy with the results. I'm now trying again, this time using the high-level variables of LaTeX3 to do things. There is going to be a cost in speed, but I hope that making the code readable will be reward enough. I'm also spotting ways to improve the flow of code, so that there should be less to actually do in the new version. Looking to the future, making the code more maintainable should more than compensate for a little loss of speed. In the end, I'm sure I'll be asked for more features, and having data structures I can rely on is essential for doing that.
