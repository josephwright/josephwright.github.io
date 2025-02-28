---
title: "The tagging project and beamer"
layout: post
permalink: /2025/02/28/the-tagging-project-and-beamer
categories:
  - tagging
---

I talked [a little while ago](/2024/09/07/tagging-project-progress) about work
that the LaTeX Project team are doing on creating tagged PDFs automatically
from 'standard' LaTeX sources. I promised to talk about how this might impact
[`beamer`](https://ctan.org/pkg/beamer), and was recently reminded about that.

## The nature of presentations

The first thing to say is that `beamer` (or rather presentations/slides) are a
tricky topic. There is lots of (legal) pressure for people doing teaching to
provide accessible resources, which includes slides (at least to some extent).
On the other hand, there are a lot of structural things that make presentations
a lot more complexes from a tagging point of view than more classical
'documents' (articles and the like). Presentations also tend to be limited-life
documents: most people will revise slides each time they present, unlike an
article that once published is basically 'frozen'. That means that the idea
that documents have to work 'unchanged' isn't quite the same for `beamer` as it
is for say the `article` class. But work does need to be done.

## Work so far

The wider reason that tagging currently doesn't work at all with `beamer` is
that internally, the class is 'interesting'. There is a lot of re-boxing
material, and very little in the way of semantic flow. The class also does
things its own way: that means that in a lot of places, standard LaTeX code is
ignored or overwritten, and so the work being done on tagging in general
doesn't apply.

Along with other members of the team, I've looked at `beamer` in detail and
we've concluded that 'upgrading' to tagging isn't realistic in the current
class. What's needed instead is a `beamer` replacement, taking forward key
ideas (and as much of the syntax as we can), but starting from the idea of 
including tagging support.

## Future plans

Writing something that covers everything `beamer` does will take a long time,
so that's not the initial target. Rather, we want to pick off specific areas.
First, the simple idea of a tagged structure that looks like a slide, then
moving on to simple overlays before even looking at the 'visual effects' that
people like to use in presentations. At the moment, the code for this effort is
not public, but once there is something that works for simple slides (like my
own teaching), that will change.

As well as the LaTeX Project team, there are a few other people with an
interest in this work. So I hope I can get things moving along once the basics
are in place.

## Document structure

There is a particular point to consider when tagging is that it makes little
sense to try to tag slides themselves, at least unless they use no
animations. If you think about a typical `beamer` slide such as
```latex
\begin{frame}
  \frametitle{Some things I did}
  \begin{itemize}[<+->]
    \item One
    \item Two
    \item Three
  \end{itemize}
\end{frame}
```
the resulting PDF will have three pages, each of which contains at least one of
the list items, and all of which have the same title. For tagging/reuse, we
almost certainly don't want that: we want the 'flattened' version (as you'd
have in an handout).

That looks OK if you take a simple example, but once authors start using
overlays to swap one image for another 'in place', _etc_., it's no longer clear
what the right tagging might be. So part of the overall project here will be
about working with users to explore what the answers are.