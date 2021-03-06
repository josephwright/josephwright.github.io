---
title: Checking over the beamer codebase
layout: post
permalink: /2017/01/08/checking-over-the-beamer-codebaes/
categories:
  - beamer
  - Packages
---
Anyone who is watching the [`beamer` GitHub repository](https://github.com/josephwright/beamer) will notice quite a lot of checkins, starting from the beginning `beamer.cls` and working forward. Most of these are 'internal' changes, so readers might wonder what is going on.

I've been involved with `beamer` for a while, but have not really taken a good look over the code yet. Several of the [entries in the issue list ](https://github.com/josephwright/beamer/issues)are quite subtle, and it's clear that a proper tidy-up of the code is needed to sort them out. That means addressing several internal inconsistencies, but it's also helpful for me to get the code into a form I'm used to. So there are a mix of cosmetic changes in with some real improvements in the code.

Hopefully I'll not introduce and new issues doing this work. However, it's not easy to avoid changing behaviour in LaTeX, especially as `beamer` is somewhat delicate in the first place. So if anyway is keen to help with the work, simply grabbing the development code from time to time and making sure it doesn't break existing presentations would be very helpful!
