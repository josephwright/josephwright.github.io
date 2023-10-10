---
title: Reworking and exposing siunitx internals
layout: post
permalink: /2014/09/18/reworking-and-exposing-siunitx-internals/
categories:
  - expl3
  - Packages
  - siunitx
tags:
  - testing
---
I've been [talking for a while](/2014/03/13/work-on-siunitx-v3/) about working on a new major version of [`siunitx`](https://ctan.org/pkg/siunitx). I've got plans to add some new features which are difficult or impossible to deliver using the v2 set up, but here I want to look at perhaps what's more important: the back end, programming set up and related matters.

I've now made a start on the [new code](https://github.com/josephwright/siunitx/tree/master), working first on what I always think of as the core of `siunitx`: the unit processor. If you take a look at the new material and compare it with the [existing release](https://github.com/josephwright/siunitx/tree/stable) the first thing that should be obvious is that I've finally made a start on splitting everything up into different sub-parts. There are at least a couple of reasons for this. First, the monolithic `.dtx` for v2 is simply too big to work with comfortably. More importantly, though, the package contains a lot of different ideas and some of them are quite useful beyond my own work. To ensure that these are available to other people, it would seem best to make the boundaries clear, and separate sources helps with that.

That leads onto the bigger picture change that I'm aiming for. As regular readers will know, I wrote the first version of `siunitx` somewhat by accident and in an _ad hoc_ fashion. Working on v2, I decided to make things more organised and also to use `expl3`, which I'd not really looked at before. So the process of writing the second version was something of a learning experience. At the same time, `expl3` itself has firmed up a lot over the time I've been working with it. As such, the current release of `siunitx` has rather a lot of rough edges. In the new code, I'm working from a much firmer foundation in terms of conventions, coding ideas and [testing implementations](/2014/05/27/testing-tex-lua-and-tex-and-not-just-for-luatex/). So for v3 I'm aiming to do several things. A key one for prospective `expl3` programmers is the idea of defined interfaces. Rather than making everything internal, this time I'm documenting code-level access to the system. That means doing some work to have clearly defined paths for information to pass between sub-modules, but that's overall a good thing. I'm also using the LaTeX3 teams new testing suite, [`l3build`](https://ctan.org/pkg/l3build), to start setting up proper code tests: these are already proving handy.

The net result of the work should be a better package for end users but also extremely solid code that can be used by other people. I'm also hopeful that the ideas will be usable with little change in a 'pure' LaTeX3 context. Documenting how things work might even have a knock-on effect in emulating `siunitx` in say [MathJax](https://github.com/mathjax/MathJax/issues/447). Beyond that, I've viewed `siunitx` as something of a sales pitch for `expl3`, and providing a really top-class piece of code is an important part of that. If I can get the code level documentation and interfaces up to the standard of the user level ones, and improve the user experience at the same time, I think I'll be doing my job there.
