---
title: "ltx-talk: A new class for presentations"
layout: post
permalink: /2025/07/12/ltx-talk-a-new-class-for-presentations
categories:
  - general
---

I've just sent the first (v0.1.0) release of
[`ltx-talk`](https://ctan.org/pkg/ltx-talk) to CTAN. This is a new
tagging-aware class which works similarly to
[`beamer`](https://ctan.org/pkg/beamer). I've [talked
before](/2025/02/28/the-tagging-project-and-beamer) about the need to write a
class from scratch for tagged presentations, so this should be no real
surprise.

This is very much a work-in-progress, so don't be surprised if things you've
used in `beamer` simply don't work. But something like
```latex
\DocumentMetadata{tagging = on}
\documentclass{ltx-talk}

\begin{document}

\begin{frame}
  \begin{itemize}[<+->]
    \item First
    \item Second
    \item Third
  \end{itemize}
\end{frame}
```
will work fine.

If you want to see a full example, I've uploaded my [lecture slides on polymer
chemistry](/uploads/2025/07/Polymers.zip), which I've updated from `beamer` to
`ltx-talk` for teaching in the autumn.