---
title: Work on siunitx v3
layout: post
permalink: /2014/03/13/work-on-siunitx-v3/
categories:
  - Packages
  - siunitx
---
I recently posted a few ['notes to myself'](/2014/02/27/siunitx-development-notes-for-my-future-self/) about future directions in `siunitx` development. With them down in print, I've been giving them some serious thought and have made a proper start on work on version 3 of the package. I'm starting where I'm happiest: the unit parser and related code, and am working on proper separation of different parts of the code. That's not easy work, but I think it should give me a good platform to build on. I'm also working hard to make the new code show 'best practice' in LaTeX3 coding: the plan is to have much richer documentation and some test material to go with the new code. Looking forward, that should make creating a 'pure' LaTeX3 units module pretty easy: it will be a minor set of edits from what I'm working on now.

I've got a good idea of the amount of work I need to do: there are about 17k lines in the current `siunitx.dtx`, which comes out to around 7.5k lines of code. That sounds like a lot, but as much of what I need to do is more editing that writing from scratch I'm hoping for an alpha build of version 3 some time this summer.
