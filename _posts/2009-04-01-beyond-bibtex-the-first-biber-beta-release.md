---
id: 250
title: 'Beyond BibTeX: the first biber beta release'
date: 2009-04-01T19:21:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=250
permalink: /2009/04/01/beyond-bibtex-the-first-biber-beta-release/
categories:
  - biblatex
  - Packages
tags:
  - biber
  - JabRef
---
A notice in my inbox from François Charette alerted me yesterday to the first beta release of <a title="A BibTeX replacement for users of biblatex" href="http://biblatex-biber.sourceforge.net/">biber</a>. This is a cross-platform (Perl) replacement for BibTeX for <a title="Bibliographies in LaTeX using BibTeX for sorting only" href="http://www.ctan.org/pkg/biblatex">biblatex</a> users. By moving on from BibTeX, there are a number of advantages. First, the problems inherent in the BibTeX code (no Unicode support, memory limitations and so on) are removed. The need for something beyond BibTeX is a well-known problem.

More importantly, biber comes with an experimental XML file format as a replacement for the .bib file type. The limitations of the .bib approach are more subtle than those of BibTeX itself. A lot of problems stem from the simplicity of the .bib format. This severely limits how much detail can be given for complex data types. For example, there is no good way to give multiple publishers and locations in the .bib format:
<!-- {% raw %} -->
<pre>publisher = {{First Company} and {Second Company}},
location = {Town and OtherTown}</pre>
<!-- {% endraw %} -->
So which place goes with which publisher? We might assume the first with the first, the second with the second, but why not both locations for both publishers or something more complex? By starting from the biblatex experience, biber can build in this type of data from the start. Particularly in arts subjects, this looks like a great idea.

One important question is publicity. Within the LaTeX world, biblatex is still not that widely used. This is of course partly as it is still in beta. However, for biber to succeed both it and biblatex need publicity outside of LaTeX. One obvious route is to talk to the people who develop things like <a title="JabRef reference manager" href="http://jabref.sourceforge.net/">JabRef</a>, <a title="BibDesk" href="http://bibdesk.sourceforge.net/">BibDesk</a> and so on. These programmes use the .bib format to store data, but can be used without ever going near LaTeX. Other ideas are I'm sure welcome!

Over all, I'm very excited by biblatex and biber. It's clear that biblatex is a major advance for LaTeX users, and anything that makes life easier is welcome.
