---
title: Collecting environment content using xparse
layout: post
permalink: /2019/03/07/collecting-environment-content-using-xparse
categories:
  - LaTeX3
---

LaTeX environments are almost always used for cases where the content does
not make sense as a macro argument. That can happen for example because
there are clear 'start' and 'end' conditions, because the content is long
and open-ended, or because category code changes are needed.

The `amsmath` bundle first implemented an approach to collecting up the entire
content of environments. For `amsmath`, this is needed to allow two-pass
measurement of the width of `align` environments. Not surprisingly, this idea
turns out to be more widely useful. It appears in a generic form in the
[`environ`](https://ctan.org/pkg/environ) package, which allows us
to do
```LaTeX
\documentclass{article}
\usepackage{environ}
\begin{document}
\NewEnviron{foo}{\showtokens\expandafter{\BODY}}
\begin{foo}
Some content
\end{foo}
\end{document}
```
with the content of the environment referred to as `\BODY`.

There have been long-standing requests to add a similar ability to
[`xparse`](https://ctan.org/pkg/xparse).
After some consideration, the LaTeX team have now added this ability as a
new type of argument: `b`-type. Rather than requiring a separate command, this
integrates directly into the existing approach in `xparse`:
```LaTeX
\documentclass{article}
\usepackage{xparse}
\begin{document}
\NewDocumentEnvironment{foo}{b}{\showtokens{#1}}{}
\begin{foo}
Some content
\end{foo}
\end{document}
```

Probably most notable here is the fact that the environment content is
available simply as `#1`, rather than requiring a special macro name. It also means
that there are no new mechanisms to learn: we can add optional and mandatory
arguments to the environment before collecting the body.
```LaTeX
\documentclass{article}
\usepackage{xparse}
\begin{document}
\NewDocumentEnvironment{foo}{O{}mb}{\showtokens{#3}}{}
\begin{foo}[stuff]{more-stuff}
Some content
\end{foo}
\begin{foo}{even-more-stuff}
Some content
\end{foo}
\end{document}
```

Of course, there is a reason that most of the time you do not want to collect up
all of an environment. But equally there are times when you do want to do exactly
that. Adding support in `xparse` should make that a little easier.
