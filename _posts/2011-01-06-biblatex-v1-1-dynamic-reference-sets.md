---
id: 877
title: 'biblatex v1.1: dynamic reference sets'
date: 2011-01-06T19:39:39+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=877
permalink: /2011/01/06/biblatex-v1-1-dynamic-reference-sets/
categories:
  - biblatex
  - Packages
---
The latest version of <a title="Bibliographies in LaTeX using BibTeX for sorting only" href="http://ctan.org/pkg/biblatex">biblatex, v1.1,</a> appeared on <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a> yesterday. This is a feature release, not just bug fixes, and so there are lots of new things there. At the same time, <a title="Biber: BibTeX replacement for biblatex" href="http://biblatex-biber.sourceforge.net/">Biber</a> has been updated to v0.7. If you use <a title="TeX Live" href="http://www.tug.org/texlive">TeX Live 2010</a>, you'll be able to get the new biblatex using <code>tlmgr</code> in a day or so, and can get the Biber update <em>via</em> <a title="TLContrib" href="http://tlcontrib.metatex.org/">TLcontrib</a> already.

Many of the new features rely on Biber, and will not work with BibTeX. As Biber has lots of advantages anyway, including UTF-8 support and active development, this is no real hindrance.

I want to focus here on one new feature, as it's one I requested. In chemistry and physics we tend numerical reference styles and to have lots of references. Often, several of these will be related, and so can be ‘compacted’ into a single number. With traditional BibTeX styles, this can be done using the <a title="Enhanced multiple=">mciteplus</a> package and a suitable <code>.bst</code> file. biblatex has supported this using ‘reference sets’ for some time, but up to now this has required modification of the database entries. In v1.1, you can define a reference set in the preamble:
<pre>\defbibentryset{set1}{key1,key2,key3}
</pre>
and then cite the set in the document. There is also support for mciteplus-like syntax, but I think it's probably best to use the native biblatex approach here.

Compressing multiple citations in a dynamic way was really the only problem I had with using biblatex for all of my citations. Now that this is sorted, I'll be sticking to biblatex all of the time, and I'd urge other physical scientists to do the same: biblatex is a much more flexible approach than the traditional BibTeX citation system.