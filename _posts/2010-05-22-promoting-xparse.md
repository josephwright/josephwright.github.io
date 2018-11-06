---
id: 702
title: Promoting xparse
date: 2010-05-22T10:25:45+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=702
permalink: /2010/05/22/promoting-xparse/
categories:
  - LaTeX3
tags:
  - xparse
---
I've had a few chances in recent weeks to promote the <a title="Generic document command parser" href="http://ctan.org/pkg/xparse">xparse</a> package.  Regular readers will know that xparse is part of the efforts of the <a title="LaTeX3 Project" href="http://www.latex-project.org/latex3.html">LaTeX3 Project</a>, and is meant to provide a replacement for <code>\newcommand</code>, <em>etc.</em>, for creating document macros. The promotions have come up where there are things that are hard to do with <code>\newcommand</code> but easy with xparse. One example was creating an <a href="http://www.latex-community.org/forum/viewtopic.php?f=46&amp;t=8881">optional argument for a macro but giving it in normal braces</a>. With xparse, this is pretty straight forward
<!-- {% raw %} -->
<pre>\documentclass{article}
\usepackage{xparse}
\NewDocumentCommand\en{g}{%
  \IfNoValueTF{#1}{\epsilon}{\epsilon_{#1}}%
}
\begin{document}
\( \en \) and \( \en{stuff} \).
\end{document}</pre>
<!-- {% endraw %} -->
This is clear, and does not need any knowledge of the internals of the LaTeX3 approach. So I'm going to keep promoting xparse for day to day LaTeX users, even if they aren't using much code. Hopefully this will make life easier for them, and for me, and will be a real benefit now from the LaTeX3 work.
