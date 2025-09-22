---
title: "Moving on from achemso"
layout: post
permalink: /2025/09/22/moving-on-from-achemso
categories:
  - general
---

The [`achemso`](https://ctan.org/pkg/achemso) package has provided the standard
BibTeX styles following the American Chemical Society (ACS) guidelines since
before I started using LaTeX. I've looked after `achemso` since 2008, and took
it from a simple BibTeX `.bst` to a bundle including submission class, a demo
document and other goodies.

I started the class many years ago, and with hindsight some of it was not such
a great plan. More importantly, the ACS have never used LaTeX in production,
which has always meant that using a dedicated class was a bit awkward: getting
things into a specific class only for them to strip that out again. I've
therefore recently agreed with the ACS to move from a dedicated class to a
simple template, now available [on
GitHub](https://github.com/josephwright/acs-template) and soon to appear on the
ACS website. Authors can then simply use `article` with minor adjustments and
get something that is suitable for production.

At the same time, classical BibTeX styles, whilst still widely used, are
better replaced by [`biblatex`](https://ctan.org/pkg/biblatex) methods.
That opens up a lot of flexibility to the user, and avoids needing add-on
packages to provide control or compound citations.

So I'm marking `achemso` as for historical support only, and recommending all
new content shifts to updated approaches. I'll keep `achemso` working of
course: not that there should be much to do! But it's time for people to move
away from what was a rather rigid approach in new documents.