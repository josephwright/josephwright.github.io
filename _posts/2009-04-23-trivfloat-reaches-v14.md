---
title: trivfloat reaches v1.4
layout: post
permalink: /2009/04/23/trivfloat-reaches-v14/
categories:
  - Packages
---
The LaTeX kernel does not make it easy to make new types of float. As a result, packages such as [`float`](https://ctan.org/pkg/float) and [`floatrow`](https://ctan.org/pkg/floatrow) have been developed to make life easier. The [`memoir`](https://ctan.org/pkg/memoir) class includes similar functionality. However, all of these systems still require modifications to get new floats to look like the base LaTeX ones. So some time ago I wrote the [`trivfloat`](https://ctan.org/pkg/trivfloat) package, which warps all of this up into a single macro.  I've not heard much from users, so the package had not been looked at by me for about 18 months, until today.

What happened today?  An e-mail from Hinrich Goehlmann, who found a bug in the package. Hinrich was in a hurry (apparently he's got a book to get to the publishers), so I got the bug sorted and something back to him over lunch. I then decided to review the package rather more carefully, and the result is v1.4, on its way to [CTAN](https://www.ctan.org) now. I've extended the functionality a bit, added support for floatrow, tidied up the code and also fixed the bugs (I hope). I'm pleased that trivfloat is providing useful: the aim is to make users lives easier, with all of the hard work hidden away.
