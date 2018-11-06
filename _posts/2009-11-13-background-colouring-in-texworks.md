---
id: 538
title: Background colouring in TeXworks
date: 2009-11-13T08:34:58+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=538
permalink: /2009/11/13/background-colouring-in-texworks/
categories:
  - TeXworks
---
The current experimental builds of <a title="Lowering the entry barrier to the TeX world" href="http://www.texworks.org/">TeXworks</a> now include the ability to alter the background colour of text, as well as the foreground. At the moment, you can't do this in an additive fashion (varying the two independently). However, it does make it easy to have something a bit nicer than the default bright red for comments. I've altered my syntax-patterns.txt file for LaTeX to read
<pre>[LaTeX]
# special characters
darkred		N	[$#^_{}&amp;]

# LaTeX environments
darkgreen	N	\\(?:begin|end)\s*\{[^}]*\}

# LaTeX packages
darkblue	N	\\usepackage\s*(?:\[[^]]*\]\s*)?\{[^}]*\}

# control sequences
blue		N	\\(?:[A-Za-z@]+|.)

# comments
black/lightgrey			Y	%.*</pre>
You'll see that the last line includes two colours, so I get black on light grey for comments.
