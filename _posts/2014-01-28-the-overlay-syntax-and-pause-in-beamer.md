---
id: 1676
title: The +-overlay syntax and \pause in beamer
date: 2014-01-28T07:16:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1676
permalink: /2014/01/28/the-overlay-syntax-and-pause-in-beamer/
categories:
  - beamer
tags:
  - overlays
---
In a [recent post](http://www.texdev.net/2014/01/17/the-beamer-slide-overlay-concept/) I looked at how to use the `+` syntax to create flexible overlays in `beamer`. The key concept of that syntax is to allow dynamic slides to be created without having to hard-code slide numbers. The classic example is to reveal a list an item at a time:

```latex
\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
```

As I discussed in the earlier post, this is a very powerful way to create overlays (dynamic slides from the same frame source). However, a classic problem people have is combining this with the `\pause` command. For example, the following creates _four_ slides:

```latex
\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
  \pause
  Text after the list
\end{frame}
```

Why? If you read the `beamer` manual, it's all about the value of `\beamerpauses`, but if we skip to the key point, you _should not_ use `\pause` on the same slide as `&lt;+-&gt;` (or similar).

## Beyond the power of `\pause`: `\onslide`

The reason people get into trouble is I think because they imagine `\pause` as the best way to break 'running text' in a frame into overlays. However, `\pause` is really just the most basic way of breaking up frames and is meant just for the simplest cases

```latex
\begin{frame}
  Some content
  \pause
  Some more content
\end{frame}
```

The moment you introduce other dynamic behaviour, you need more control than `\pause` offers. Indeed, this is pretty clear in the `beamer` manual: what people are actually looking for is `\onlside`.

Unlike `\pause`, which only knows some basic stuff about slide numbers, `\onslide` works with the full power of the flexible overlay specification (indeed, an overlay specification is required). So to get text after a list, what is needed is

```latex
\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
  \onslide&lt;+-&gt;
  Text after the list
\end{frame}
```

As we are then using the special `+` syntax for all of the overlays, everything is properly tied together and will give the (probably) expected result: three slides.

The `beamer` manual covers other more complex effects using `\only`, `\uncover`, `\alt` and so on, but using `\onslide` you can do everything you _think_ you can do with `\pause` but actually have it work when using the `+` syntax on the slide too!
