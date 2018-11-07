---
title: Promoting xparse
layout: post
permalink: /2010/05/22/promoting-xparse/
categories:
  - LaTeX3
tags:
  - xparse
---
I've had a few chances in recent weeks to promote the [`xparse`](https://ctan.org/pkg/xparse) package.  Regular readers will know that `xparse` is part of the efforts of the [LaTeX3 Project](https://www.latex-project.org/latex3.html), and is meant to provide a replacement for `\newcommand`, _etc._, for creating document macros. The promotions have come up where there are things that are hard to do with `\newcommand` but easy with `xparse`. One example was creating an [optional argument for a macro but giving it in normal braces](http://www.latex-community.org/forum/viewtopic.php?f=46&amp;t=8881). With `xparse`, this is pretty straight forward

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage{xparse}
\NewDocumentCommand\en{g}{%
  \IfNoValueTF{#1}{\epsilon}{\epsilon_{#1}}%
}
\begin{document}
\( \en \) and \( \en{stuff} \).
\end{document}
```
<!-- {% endraw %} -->

This is clear, and does not need any knowledge of the internals of the LaTeX3 approach. So I'm going to keep promoting `xparse` for day to day LaTeX users, even if they aren't using much code. Hopefully this will make life easier for them, and for me, and will be a real benefit now from the LaTeX3 work.
