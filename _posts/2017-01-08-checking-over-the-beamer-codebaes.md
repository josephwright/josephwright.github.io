---
id: 2091
title: Checking over the beamer codebase
date: 2017-01-08T22:43:55+00:00
author: josephwright
layout: post
guid: https://www.texdev.net/?p=2091
permalink: /2017/01/08/checking-over-the-beamer-codebaes/
categories:
  - beamer
  - Packages
---
Anyone who is watching the <a href="https://github.com/josephwright/beamer"><code>beamer</code> GitHub repository</a> will notice quite a lot of checkins, starting from the beginning <code>beamer.cls</code> and working forward. Most of these are 'internal' changes, so readers might wonder what is going on.

I've been involved with <code>beamer</code> for a while, but have not really taken a good look over the code yet. Several of the <a href="https://github.com/josephwright/beamer/issues">entries in the issue list </a>are quite subtle, and it's clear that a proper tidy-up of the code is needed to sort them out. That means addressing several internal inconsistencies, but it's also helpful for me to get the code into a form I'm used to. So there are a mix of cosmetic changes in with some real improvements in the code.

Hopefully I'll not introduce and new issues doing this work. However, it's not easy to avoid changing behaviour in LaTeX, especially as <code>beamer</code> is somewhat delicate in the first place. So if anyway is keen to help with the work, simply grabbing the development code from time to time and making sure it doesn't break existing presentations would be very helpful!