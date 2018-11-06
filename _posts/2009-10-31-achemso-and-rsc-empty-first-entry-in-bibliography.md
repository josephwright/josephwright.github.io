---
id: 528
title: 'achemso and rsc: empty first entry in bibliography'
date: 2009-10-31T09:07:18+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=528
permalink: /2009/10/31/achemso-and-rsc-empty-first-entry-in-bibliography/
categories:
  - achemso
  - Packages
tags:
  - bibliography
  - rsc
---
I've had a few e-mails recently from users of my <a title="Support for American Chemical Society journal submissions" href="http://ctan.org/pkg/achemso">achemso</a> and <a title="BibTeX styles for Royal Society of Chemistry and Wiley journals" href="http://ctan.org/pkg/rsc">rsc</a> packages, complaining that they get an empty first entry in the bibliography. Some of the users have noticed that it seems to be linked to the special control citation that both packages use. However, this is not a bug in either bundle, but is because the users have done a self-install of the packages.

In both cases, the LaTeX packages are designed to work with matching BibTeX styles. What tends to happen is people install the LaTeX stuff manually, but forget the BibTeX part. So the wrong .bst files get used by BibTeX, and odd results are seen. So my advice is, if you update anything by hand, make sure you install all of the update and not just some of it!
