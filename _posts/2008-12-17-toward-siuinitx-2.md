---
title: Toward siunitx 2
layout: post
permalink: /2008/12/17/toward-siuinitx-2/
categories:
  - Packages
  - siunitx
---
My [`siunitx`](https://ctan.org/pkg/siunitx) package has attracted a lot of attention, and I've had a lot of requests for new features.  To get these working, I'm having to re-code the package from the ground up.  There are lots of problems with the code as it stands, as it is cobbled together from the previous packages in many cases.

So far,  I've recoded the system that parses numbers, taking out a lot of the loops and making it hopefully much faster.  I've also got about half of the table system redone: this collects up the table contents in a more efficient (and intelligent) manner than the old code.  The next step is to look at the output formatting system, where I have several ideas to make everything smoother.

One area that I'm keen to improve is the user options. The current system is too complex, so I'm looking at doing something tree-based. The options are all being divided into groups, which should make things easier to follow.

Another area for lots of attention is table output.  This seems to be the thing that I get most questions about. Lots to work on there, but so far nothing is done.  I need to look over all of the suggestions I've had and find a way to please everyone (not easy).
