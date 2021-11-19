---
title: "Beyond BibTeX: the first Biber beta release"
layout: post
permalink: /2009/04/01/beyond-bibtex-the-first-biber-beta-release/
categories:
  - biblatex
  - Packages
tags:
  - Biber
  - JabRef
---
A notice in my inbox from François Charette alerted me yesterday to the first beta release of [Biber](http://biblatex-biber.sourceforge.net/). This is a cross-platform (Perl) replacement for BibTeX for [`biblatex`](https://ctan.org/pkg/biblatex) users. By moving on from BibTeX, there are a number of advantages. First, the problems inherent in the BibTeX code (no Unicode support, memory limitations and so on) are removed. The need for something beyond BibTeX is a well-known problem.

More importantly, Biber comes with an experimental XML file format as a replacement for the `.bib` file type. The limitations of the `.bib` approach are more subtle than those of BibTeX itself. A lot of problems stem from the simplicity of the `.bib` format. This severely limits how much detail can be given for complex data types. For example, there is no good way to give multiple publishers and locations in the `.bib` format:

<!-- {% raw %} -->
```
publisher = {{First Company} and {Second Company}},
location = {Town and OtherTown}
```
<!-- {% endraw %} -->

So which place goes with which publisher? We might assume the first with the first, the second with the second, but why not both locations for both publishers or something more complex? By starting from the `biblatex` experience, Biber can build in this type of data from the start. Particularly in arts subjects, this looks like a great idea.

One important question is publicity. Within the LaTeX world, `biblatex` is still not that widely used. This is of course partly as it is still in beta. However, for Biber to succeed both it and `biblatex` need publicity outside of LaTeX. One obvious route is to talk to the people who develop things like [JabRef](http://jabref.sourceforge.net/), [BibDesk](http://bibdesk.sourceforge.net/) and so on. These programs use the `.bib` format to store data, but can be used without ever going near LaTeX. Other ideas are I'm sure welcome!

Over all, I'm very excited by `biblatex` and Biber. It's clear that `biblatex` is a major advance for LaTeX users, and anything that makes life easier is welcome.
