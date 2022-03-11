---
title: siunitx v3.1 development
layout: post
permalink: /2022/03/11/siunitx-v3-1-development
categories:
  - siunitx
---

I've now done 49 (!) minor releases of [`siunitx`](https://ctan.org/pkg/siunitx)
on the v3.0.x branch. These have addressed quite a few minor bugs: I expected
to have to do a bit of work since the shift from v2 was quite major.

Things are now settling down: the open issues I've had recently are mainly
on the border of feature requests, and there don't seem to be additional
changes I've introduced by accident. With the [TeX
Live](htttps://tug.org/texlive) freeze coming up, now looks like an excellent
time to turn my thoughts to `siunitx` v3.1. The plan there is to deal with two
areas:

- Small requests that are clearly additions not bugs, so need API extensions
  but are easy/low risk
- Pick off one of the bigger requests, probably either multi-part uncertainties
  or parsing 'free form' units, or both if they are sufficiently
  straight-forward

Of course, that doesn't rule out further bugs to be fixes in the v3.0 branch:
I will continue to fix things that come up there.

Depending on how the big issues go, I might manage a v3.1 release in the summer
(June-August).
