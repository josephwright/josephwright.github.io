---
id: 81
title: The LaTeX3 “template” concept
date: 2009-01-05T17:43:21+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=81
permalink: /2009/01/05/the-latex3-template-concept/
categories:
  - LaTeX3
---
The “template” concept, implemented in the [LaTeX3](https://www.latex-project.org/latex3.html) template module, has confused me for a while. I've had a few attempts at reading the documentation, but have consistently failed to fully understand things. A recent post on the [LaTeX3 mailing list](https://listserv.uni-heidelberg.de/cgi-bin/wa?A0=LATEX-L) has prompted me to have another go at understanding things: I think that this time I might have got it.

The idea of templates is to separate the design decisions about document elements from both the user interface and the underlying coding. A template is a generalised description of a type of document element; a specific instance of a template is created for each specific use.

For example, if we have a template “SectionHead” as a generalised section-starting function, then specific instances might be Plain, Indented, Fancy, and so on. Notice that this is not the same as the user interface (where we'd expect to see `\section`, `\subsection`, _etc_.: this mapping is handled separately).

The current method for implementing templates uses a key–value method. So in our example, there will be keys for things like the font weight of the text, the surrounding whitespace and so on. When an instance of a template is created, so of these values are set, so that the instance will work more rapidly. Other values are left until run-time, and so can be set by the user.

Once you understand the concept, this looks like a very clever way of keeping design and code more-or-less independent. Of course, this does depend on how many template settings are available to the designer. I'm not too sure about the method for creating keys of different types, as it is not quite classical keyval and is therefore something I'm not used to (but perhaps as I'm a big fan of [`pgfkeys`](https://ctan.org/pkg/pgf) I would say that). Perhaps it will grow on me.
