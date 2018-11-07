---
title: LaTeX3 snapshot release
layout: post
permalink: /2009/06/09/latex3-snapshot-release/
categories:
  - LaTeX3
---
The [LaTeX3 Project](https://www.latex-project.org/latex3.html) (of which I'm a member) have made a snapshot release of the current [LaTeX3 code](https://www.latex-project.org/code.html) to [CTAN](https://www.ctan.org) today. This is in two parts:

- [`expl3`](https://ctan.org/pkg/expl3), the base layer for LaTeX3, which provides a consistent programming interface for LaTeX3 on top of TeX (or rather, on top of [pdfTeX](http://www.pdftex.org), [XeTeX](https://tug.org/xetex/) or [LuaTeX](http://www.luatex.org)).
- [`xpackages`](https://ctan.org/pkg/l3packages), higher level interface ideas for LaTeX3.

`expl3` is now reasonably stable: the code has been carefully reviewed and the Team are happy that what is there works well. There are gaps, and some of these are definitely on the 'to do' list. On the other hand, the `xpackages` bundle is not so close to being finished. At the moment, it includes only the parts of the experimental code that look the closest to reaching some kind of conclusion. However, it is also the part that is actively being reviewed at the moment. So I expect changes!

I'm hoping that as `expl3` gets distributed around the TeX world it will be possible to consider using it for coding new packages. The ideas in `expl3` make coding much easier, over all, even if initially there is a lot to learn. Of course, delivering more of LaTeX3 will help in getting people interested as well. That is something I'm definitely keen on.
