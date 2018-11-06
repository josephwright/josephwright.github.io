---
id: 1367
title: LaTeX3 gets a new FPU
date: 2012-05-15T15:58:38+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1367
permalink: /2012/05/15/latex3-gets-a-new-fpu/
categories:
  - LaTeX3
tags:
  - floating point
---
For a while now we've been promising to update the floating point functions in LaTeX3 to provide an expandable approach to calculations. We are now making good progress in swapping the old code for the new material. There are still a few things to be decided, but the general plan looks pretty clear.

The new code lets you parse floating point expressions in the same way you can for integers. So you can write

```latex
\fp_eval:n { 10 / 3  + 0.35 }
```

and get the output

```
3.683333333333333
```

without needing to worry about working with dimensions. Even more usefully, there are a range of built in mathematical functions, so things like

```latex
\fp_eval:n { sin ( pi / 3 ) }
```

gives

```
0.8660254037844386
```

as you'd want.

You might pick up from the above output that the new FPU works to a higher accuracy than the old one: 16 significant figures. That's been done without a bad performance hit: great credit goes to Bruno Le Floch for the work on this. Of course, you don't have to have 16 figure output: the code includes rounding functions and various display options, so for example

```latex
\fp_eval:n { round ( sin ( pi / 3 ) , 3 ) }
```

At the moment you'll have to grab the latest [development code](https://github.com/latex3/svn-mirror) to get this new version as part of expl3, but it will be in the next [CTAN](https://www.ctan.org) snapshot some time in June. You might also find that not every function you want implemented is available: for example, there are currently no inverse trigonometric functions. Those are all on the to do list, but there not needed for typesetting so may be a little while.
