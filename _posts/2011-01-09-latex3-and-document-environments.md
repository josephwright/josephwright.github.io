---
id: 883
title: LaTeX3 and document environments
date: 2011-01-09T11:17:28+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=883
permalink: /2011/01/09/latex3-and-document-environments/
categories:
  - LaTeX3
tags:
  - environments
  - xparse
---
There was a [question](http://tex.stackexchange.com/questions/8528/) on the [{TeX} Q&amp;A site](http://tex.stackexchange.com/) recently about compiling a document reading

```latex
\documentclass{minimal}
\document
a
\enddocument
```

This doesn't work: I've explained why as my answer to the question. I also mentioned that in [LaTeX3](http://www.latex-project.org/latex3.html) I'd expect this won't work. Here, I want to look at that in a bit more detail.

First, the background. When LaTeX2e creates an environment `foo`, what actually happens is two macros called `\foo` and `\endfoo` are defined (hence the original question). When you do

```latex
\begin{foo}
...
\end{foo}
```

LaTeX looks for the `\foo` macro, and if it finds it starts a group and inserts `\foo`. At the end of the environment, LaTeX will use `\endfoo` if it exists, but this is not required.

There are some problems with this scheme. First, it's possible to abuse the system, as something like

```latex
\begin{emph}
...
\end{emph}
```

will not raise an error even though `\emph` was never intended to be used as the start of an environment. (LaTeX2e does not require that `\endemph` exists here: it's only the start of an environment which must be defined.) Secondly, due to this mixing it's not possible to have a `foo` environment and independent `\foo` macro: the two are tied together. Finally, as `\endfoo` is ‘special’ `\newcommand` won't let you create macros which start `\end...`.

For LaTeX3, we want the approach to be different. Document commands and document environments should be independent of one another, and so [`xparse`](https://ctan.org/pkg/xparse) defines a pair of special internal macros when you use

```latex
\NewDocumentEnvironment{foo}...
```

This is totally independent of a macro called `\foo`, so the plan is that you'll be able to have an environment called `foo` and a separate `\foo` command, or indeed one called `\endfoo`.

At present, most people will be using xparse with LaTeX2e. That means we still need to follow what LaTeX2e does. So at the moment you're not going to see the change: messing with the LaTeX2e mechanism looks like a very bad idea. However, for a native LaTeX3 format the clash will disappear.
