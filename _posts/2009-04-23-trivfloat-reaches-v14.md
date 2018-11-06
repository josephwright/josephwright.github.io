---
id: 278
title: trivfloat reaches v1.4
date: 2009-04-23T21:49:22+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=278
permalink: /2009/04/23/trivfloat-reaches-v14/
categories:
  - Packages
---
The LaTeX kernel does not make it easy to make new types of float. As a result, packages such as <a title="Improved interface for floating objects" href="http://www.ctan.org/pkg/float">float</a> and <a title="Modifying the layout of floats" href="http://www.ctan.org/pkg/floatrow">floatrow</a> have been developed to make life easier. The <a title="Typeset fiction, non-fiction and mathematical books" href="http://www.ctan.org/pkg/memoir">memoir</a> class includes similar functionality. However, all of these systems still require modifications to get new floats to look like the base LaTeX ones. So some time ago I wrote the <a title="Quick float definitions in LaTeX" href="http://www.ctan.org/pkg/trivfloat">trivfloat</a> package, which warps all of this up into a single macro.  I've not heard much from users, so the package had not been looked at by me for about 18 months, until today.

What happened today?  An e-mail from Hinrich Goehlmann, who found a bug in the package. Hinrich was in a hurry (apparently he's got a book to get to the publishers), so I got the bug sorted and something back to him over lunch. I then decided to review the package rather more carefully, and the result is v1.4, on its way to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a> now. I've extended the functionality a bit, added support for floatrow, tidied up the code and also fixed the bugs (I hope). I'm pleased that trivfloat is providing useful: the aim is to make users lives easier, with all of the hard work hidden away.
