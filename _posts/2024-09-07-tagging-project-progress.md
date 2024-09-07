---
title: "Tagging project progress"
layout: post
permalink: /2024/09/07/tagging-project-progress
categories:
  - tagging
---

The [LaTeX Project](https://www.latex-project-org/) have been working for about
4 years now on creation of automatically tagged PDFs from (more-or-less)
unmodified LaTeX documents. We've been reporting regularly in _LaTeX News_, and
things are moving forward nicely.

We (Frank, Ulrike and I) went to the recent [DocEng
2024](https://www.documentengineering.org/doceng2024) conference in San José.
Ulrike presented a workshop showing what is doable right now with the updated
code. At present, this is still an opt-in testphase, but most of the time
```latex
\DocumentMetadata{testphase = {phase-III,firstaid,math,table,title}}
```
is enough to use it. As you can probably tell, this uses the current (phase
III) code plus add-ons for maths, tables and titles: that is all a bit more
experimental but is worth exploring.

We are building up an idea of which packages and classes work out-of-the-box
with the latest code: you can [view the current list online](
https://latex3.github.io/tagging-project/tagging-status/). It's amazing how many
packages already work, but of course there is work to do. I've got some
adjustments to make for [`siunitx`](https://ctan.org/pkg/siunitx), but as the
tagging structures are still not finalised, I'm waiting a bit. We also need to
look at performance: tagging takes time, but when we make it opt-out we need it
to be as fast as possible.

On the to-do list here is `beamer`: a complex class with a lot of challenges! I
think that deserves it's own post, so I'll return to that soon in a dedicated
post.

But for day-to-day use, I'm finding tagging something I can mainly switch on
and just use. So other than slides, all of my LaTeX work is now tagged - may
not perfectly just yet, but each release getting better and better.