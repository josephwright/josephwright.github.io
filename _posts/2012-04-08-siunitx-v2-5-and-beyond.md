---
title: siunitx: v2.5 and beyond
layout: post
permalink: /2012/04/08/siunitx-v2-5-and-beyond/
categories:
  - Packages
  - siunitx
---
Anyone who watches the [BitBucket site](https://github.com/josephwright/siunitx) for [`siunitx`](https://ctan.org/pkg/siunitx) development will have noticed that I've been adding a few new features. As I've done for every release in the 2.x series, new options means a new minor revision, and so these will all be in v2.5. I've also revised some of the behaviour concerning math mode, so there are now very few options which automatically assume math mode.

Looking beyond v2.5, I have some bigger changes I'd like to make to `siunitx`. When I initially developed the package, it was very much a mixture of things that seemed like a good idea. The work for version 2 meant a lot of changes, and a lot more order. However, I've learnt more about units, LaTeX and programming since then, and that means that there are more changes to think about.

The internal structure is quite good, but I need to work on some parts of the code again. For users, of course, that won't show up, but it is important to me. It's also not so straight-forward: the `.dtx` is about 17 000 lines long! However, there are also some issues at the user level. In particular, I think I've offered too many options in some areas, for example font selection. Revising those will alter behaviour, but it will also improve performance and the clarity of some edge cases. However, that is not such easy work and will take a while. I've got lots of other TeX commitments (plus of course a life beyond LaTeX), so these changes will wait a while yet. So once v2.5 is finalised I'd expect to have little change in `siunitx` for some time: probably until at least the autumn, and quite possibly the end of the year.
