---
title: Beamer overlays beyond the \visible
layout: post
permalink: /2014/10/13/beamer-overlays-beyond-the-visible/
categories:
  - beamer
  - Packages
---
I wrote earlier this year about [using the `beamer` overlay concept with relative slide specifications](/2014/01/28/the-overlay-syntax-and-pause-in-beamer/) to produce dynamic slide structures. Another [question about overlays](https://tex.stackexchange.com/questions/205625/) came up recently on TeX StackExchange, but this time wanting to do something a bit different.

The 'standard' `beamer` overlay system does the same as the `\visible` command: makes things appear and disappear, but always keeps space for them on the slide. However, `beamer` also provides `\only`, which completely omits items not visible on a slide. So the question was how to combine this idea with the general overlay concept.

It turns out that this is all quite straight-forward if you know what to look for. The standard `beamer` overlay syntax, for example

```latex
\item<+->
```

extends to include an action type to specify what the overlay should do. That is given as a keyword and an `@` before the overlay number(s). So for example

```latex
\begin{itemize}
  \item First item
  \item<only@1> Second item
  \item<only@2> Replacement second item
...
```

will show `Second item` on the first slide then replace it entirely with `Replacement second item` on the second slide. That approach can be combined with the idea of relative slide specs, as I talked about before, to give something like

```latex
\documentclass{beamer}
\begin{document}
   \begin{frame}
   \begin{itemize}[<+->]
      \item item 1
      \item item 2
      \item<only@+-.(2)> item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
```

to have the 'normal' items appear one at a time but with `item 3` only on slides 3 and 4.

This doesn't just apply to `only`: other keywords that work here include `visible` and `alert`. The latter tends to be seen with another syntax element: `|` to separate out appearance from a second action. A classic example of that is

```latex
\documentclass{beamer}

\begin{document}
   \begin{frame}
   \begin{itemize}[<+->]
      \item item 1
      \item item 2
      \item<+-|alert@+(1)> item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
```

where `item 3` appears on the third slide and is highlighted on the fourth one. (Note that both `+` substitutions in this line use the _same_ value for the pause counter, hence needing the `(1)` offset.) That's useful even without the 'one at a time' effect, with for example

```latex
\documentclass{beamer}

\begin{document}
   \begin{frame}
   \begin{itemize}
      \item item 1
      \item item 2
      \item<alert@+(1)> item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
```

highlighting the item on the second slide.

A bit of imagination with this syntax can cover almost any appearance/disappearance/highlight requirement. As I said before: the key thing is not to overdo it!
