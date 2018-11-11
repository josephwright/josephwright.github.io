---
title: Chemistry journals: publishers support of LaTeX
layout: post
permalink: /2010/01/05/chemistry-journals-publishers-support-of-latex/
categories:
  - General
tags:
  - chemistry
---
As the author of the [`achemso`](https://ctan.org/pkg/achemso) bundle (for supporting submissions to the [American Chemical Society](http://www.acs.org/)), I get a few queries about the support various publishers provide for LaTeX. Unlike more physics-focussed journals, the chemistry journals never typeset directly from authors LaTeX sources.  As a result, the acceptance of LaTeX material from authors is rather less popular, and tends to be patchy. So I thought I'd summarise things as I currently understand them.

## American Chemical Society (ACS)

As I said above, I've written the [`achemso`](https://ctan.org/pkg/achemso) bundle specifically for submissions to the ACS. However, while the central office are happy to host a copy on their website and so on, the ACS don't officially support the bundle. That means, in practice, that some journals are happier with LaTeX submissions than others. Each journal has its own office, and so I hear different things from people submitting to different journals. It also means that I have to pick up the requirements of each office based on feedback _via_ authors, rather than getting any formalised instructions. There are mistakes in the `achemso` bundle, and there are also requirements that I don't know about. So feedback is always useful (good or bad).

## Royal Society of Chemistry (RSC)

The RSC have rather less information about LaTeX on their website than the ACS. They do mention TeX, but only very briefly. I've written some BibTeX styles, and a very basic article template, which are available in the [`rsc`](https://ctan.org/pkg/rsc) bundle. I've had a bit of feedback on these, and I hope that they at least provide a starting point for writing a submission to the RSC in LaTeX. More generally, I think the best advice is to check with the editorial office for the relevant journal before writing anything, and to stick to the basic LaTeX article class when you do.

## Wiley

As with the RSC, Wiley don't have a lot of LaTeX information. What they _do_ say is that they only accept PDF submissions: you can't send your source. They also say to stick to the plain article class, and basically to keep things simple.

## Elsevier

Elsevier have recently had a new class written for journal submissions, [`elsarticle`](https://ctan.org/pkg/elsarticle). From what I can make out on their site, you can use this for most of their journals, which should include the chemistry ones. As this has actually been written for them to order, I imagine that Elsevier is the best place to be sending LaTeX submissions to. Hopefully other publishers will see that they have made life easier for their authors and will take note.
