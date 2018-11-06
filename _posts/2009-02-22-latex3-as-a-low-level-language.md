---
title: LaTeX3 as a low-level language
layout: post
permalink: /2009/02/22/latex3-as-a-low-level-language/
categories:
  - LaTeX3
tags:
  - LuaTeX
  - microkernel
---
There is quite a lot going on with the low level code for [LaTeX3](https://www.latex-project.org/latex3.html) at the moment. The number of commits to the code is ticking over nicely, as the code is revised and Will Robertson gets the test system written. Will has taken on a thankless task with this job, and I think is owed a debt of gratitude by everyone interested in LaTeX3.

One thing that is clear is that LaTeX3 (at the low level) is a programming language in itself, distinct from TeX. This is something of a risk, as it means that you cannot simply take what is done currently and convert it to the new system without thinking. On the other hand, the idea is to provide a system which makes programming easier and clearer, with some of the “features” of TeX hidden underneath a working LaTeX3 layer. The aim is that expansion and the somewhat odd methods for assignment to low-level TeX variables become something only the kernel team need to worry about.

It seems to me that there is a “window of opportunity” for the kernel team to show that something can be delivered, and that LaTeX3 as a programming language is the way to do this. The arrival of [LuaTeX](http://www.luatex.org/) will bring real programming to TeX: [Karl Berry](http://freefriends.org/~karl/) has pointed out that this will bring programmers to the TeX world who would never consider writing serious (La)TeX code. So I think that LaTeX3 needs to show that the language is viable before widespread take-up of LuaTeX means that no-one is interested.

With the LaTeX3 low-level language approaching stability, I'd suggest the team need to make the next step and move on to document design and user macros. There are lots of ways this could be done, but an obvious one would be to produce a “microkernel”. By this, I mean something which can do the same as:

```latex
\documentclass{minimal}
\begin{document}
Hello World!
\end{document}
```

without using LaTeX2ε at all. I'd expect the user syntax to change a bit, but in essence the minimal LaTeX document is not going to change (at least, not if LaTeX3 is to succeed).

The experts will know that there is quite a lot of work to get to the test file I've suggested, and so going from where LaTeX3 is now to a working microkernel is non-trivial. However, it would be a good opportunity to demonstrate that real (usable) progress is happening, and would also avoid the problems associated with trying to build everything from the bottom up with no top level in sight. A microkernel would show that delivery is possible, and I hope raise interest in LaTeX3 from the current _and potential_ development community.

Of course, a microkernel will still leave a lot to do. However, with something to build on I'd expect interest and ideas to accumulate and the new system to grow reasonably fast.
