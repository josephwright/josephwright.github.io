---
id: 608
title: Asking for help
date: 2010-01-21T20:28:46+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=608
permalink: /2010/01/21/asking-for-help/
categories:
  - General
---
I get quite a few e-mails asking for help with my packages, and also  spot a few questions in various public places ([comp.text.tex](http://groups.google.com/group/comp.text.tex/topics) and [The LaTeX Community](http://www.latex-community.org/forum/),  mainly). I'm always happy to help where I can, and it always makes my  life a bit easier if the question arrives with all the information to  start with.

One of the things that get repeated by almost everyone trying to help  out users is the need for a [minimal example](http://www.tex.ac.uk/cgi-bin/texfaq2html?label=minxampl). For LaTeX, that typically  looks something like:

```latex
\documentclass{article} % Or perhaps memoir, beamer, ...
\usepackage{...}
\begin{document}
Example here
\end{document}
```

ConTeXt examples are not dissimilar, while plain TeX ones need very  little at all (but I get very few of these). It's much faster to supply  everything to start with than to send a snippet with key details left out. It's surprising how many things people simply assume are obvious, when they are not (“Surely everyone uses package wibble”).

Another useful thing to do in advance of sending a query is to send a log file. Again, LaTeX users are normally best advised to include `\listfiles` in their input, so the kernel makes a neat listing of everything in use (hopefully including the versions).

Often, I get description of either how things should look or why they are wrong, rather than an actual example. If at all possible, a “reference rendering” is much easier to follow. That can be something done in a drawing programme, using some alternative (but awkward) TeX code, or a screenshot of something.  Describing things in words (especially if the questioner is not a native English speaker) can be a recipe for a long and painful process.

For questions posted in public, it's always best to drop me a line so I spot it: I do my best but sometimes I miss things. For places such as comp.text.tex, that can simply be a CC on the posting, or for forums a quick note that says

> Hello,
>
> I posted a question about your &lt;whatever&gt; package:
>
> http://some-url-here/
>
> Please take a look.

will make sure that the issue gets me interest.

On the other hand, questions direct to me obviously get straight to the point but miss out on the public record part of a posting to Usenet. The same issues do tend to pop up more than once! Sometimes there is good reason for avoiding public postings: I get questions including unpublished material about [`achemso`](https://ctan.org/pkg/achemso), for example. So I'd encourage anyone with an issue they think is general (such as a bug in one of my releases) to post something in public if possible. I always try to follow up postings as well as e-mailing people directly as well.

As I say, I'm always happy to try to help. I hope that most of the time I succeed.
