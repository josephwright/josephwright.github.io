---
id: 112
title: 'LaTeX3: Key points'
date: 2009-01-19T08:25:25+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=112
permalink: /2009/01/19/latex3-key-points/
categories:
  - LaTeX3
---
A <a href="http://www.texdev.net/2009/01/11/xetex-and-luatex-directions/#comment-41">comment</a> on one of my other posts raises the important issue of what the key targets are for <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a>. Only the team can answer this, but reading the project <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">webpage</a>, the <a title="LaTeX3 Mailing List" href="https://listserv.uni-heidelberg.de/cgi-bin/wa?A0=LATEX-">mailing list</a> and the <a title="LaTeX3 Code" href="http://www.latex-project.org/svnroot/experimental/trunk/">code</a>, you can get some ideas.
<ol>
 	<li>A well-designed, consistent and documented coding system. This is the most complete part of the current code base. The expl3 module provides a lot of low-level coding methods, which deal much better with control of expansion than using plain TeX or LaTeX2e (no long <code>\expandafter</code> runs). As I've said in <a href="http://www.texdev.net/2009/01/18/taking-good-practice-from-latex3/">another post</a>, there are ideas that you can take from this for current work.</li>
 	<li>A much larger and more functional kernel. The current LaTeX kernel provides only a limited number of functions and customisation possibilities. This is one reason for the very large number of LaTeX packages around. The new kernel will need to cover a large amount of what goes on in packages under LaTeX2e. This is much more the <a title="ConTeXt Wiki" href="http://wiki.contextgarden.net">ConTeXt</a> model, with the core team providing most of the basics.</li>
 	<li>Internal macros taking a clear and fixed number of arguments. Currently, a lot of coding and design decisions are mixed together. User macros take optional arguments and various complex ways are used to send these through to the underlying functions. The idea for LaTeX3 is that there will be a “glue” layer, which converts from user to internal syntax. At the internal level, each function will have a strictly fixed set of arguments, and the glue layer will provide those from user input.</li>
 	<li>Separation of design from code (and day-to-day use). The current kernel has design decisions all over the place: in the kernel, in classes, in packages and in documents. The LaTeX3 team are aiming for a system where functions are general, and make no assumptions about design. The glue layer described in (3) then brings in design decisions, which again are separated from user macros. Exact details are still some way off (although <a href="http://www.texdev.net/2009/01/05/the-latex3-template-concept/">template</a> shows a way of doing things).</li>
 	<li>User syntax decoupled from internal design. It seems likely that the main user “interface” to LaTeX3 will remain a file starting <code>\documentclass</code> and ending <code>\end{document}</code>. However, the ideas in (3) and (4) mean that it should be possible to use a different glue layer to typeset completely different user input with the LaTeX3 kernel. This should allow LaTeX3 to take on entirely different, but structured, input formats (most obviously XML-based).</li>
 	<li>New ideas for complex layouts. A lot of work is going into areas such as grid typesetting and complex float handling. This is intimately bound up with the output routine, and so LaTeX3 will provide a totally revised system in this area.</li>
</ol>
There are a lot of challenges there, and progress in different areas is variable. A lot of the work, of course, is in the thinking stage rather than writing the code. I'd say that all of these ideas are good things, and so it only remains to implement them all!
