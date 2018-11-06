---
id: 450
title: A model dtx file
date: 2009-10-06T16:52:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=450
permalink: /2009/10/06/a-model-dtx-file/
categories:
  - General
tags:
  - DTX
---
In my previous post, I've tried to give a very general overview of how the dtx file format comes about, from a combination of the syntax of DocStrip and ltxdoc. The problem with the bald details is that there are still lots of way to actually use the ideas to construct a dtx. So here I'm going to detail a model dtx, which is ready to be filled in with real code and documentation. The entire file is <a href="http://www.texdev.net/wp-content/uploads/2009/10/demopkg.dtx">available here as demopkg.dtx</a>: get it now if you are impatient!

The idea of constructing a dtx file in the way I'll describe is that it lets us achieve several things in one go:
<ul>
	<li>All of the files for a package can be derived from a single source (unless you need a binary, of course).</li>
	<li>The README is included in the dtx, with this useful information at the start.</li>
	<li>The ins file is included in the dtx, so the file is self-extracting.</li>
	<li>Running <code>(pdf)tex <em>&lt;name&gt;</em>.dtx</code> extracts the code and associated files (ins, README, <em>etc</em>.).</li>
	<li>Running <code>(pdf)latex <em>&lt;name&gt;</em>.dtx</code> does the extraction then typesets the documentation. This way, the documentation always has the latest code available, and users don't need to worry about which method they use to get stuff extracted.</li>
</ul>
Most of the ideas here are not mine: Will Robertson came up with a lot of this. I'm just going to give some details of what is going on. I'm going to present the source in order, with a section of the source followed by some comments explaining what is going on. I'm going to call the demonstration package ‘demopkg’: something easy for search and replace. Where ever possible, <code>\jobname</code> is used in the source so that the file name changes automatically when moving from one package to another.
<pre>% \iffalse meta-comment
% !TEX program  = pdfLaTeX</pre>
The file starts off with an <code>\iffalse</code> which will mean that ltxdoc will skip all of this code when typesetting the document. I use <a title="Lowering the entry barrier to the TeX world" href="http://www.texworks.org">TeXworks</a> as my editor, so I include the special <code>!TEX program</code> comment so that it defaults to pdfLaTeX with all of my files: this does no harm so may as well be there. The same comment is also recognised by <a title="TeXShop" href="http://www.uoregon.edu/~koch/texshop/">TeXShop</a>.
<pre>%&lt;*internal&gt;
\iffalse
%&lt;/internal&gt;</pre>
There is then a guard called ‘internal’: this is never extracted out, but lets us have an uncommented <code>\iffalse</code> in the code. which will mean that the next section will be ignored by TeX initially. The idea here is that we are going to have some text (the README), that TeX would otherwise try to typeset. We don't want that, so need to skip it at the moment.
<pre>%&lt;*readme&gt;
----------------------------------------------------------------
demopkg --- description text
E-mail: you@your.domain
Released under the LaTeX Project Public License v1.3c or later
See http://www.latex-project.org/lppl.txt
----------------------------------------------------------------

Some text about the package: probably the same as the abstract.
%&lt;/readme&gt;</pre>
This part is pretty obvious: the README file for the package, inside guards called ‘readme’. As you might expect, this will get extracted out later as the README file.  In the initial TeX run, this text will be skipped (because of the <code>\iffalse</code>), but when DocStrip runs it will show up (as DocStrip will ignore the <code>\iffalse</code>, which is in a different set of guards).
<pre>%&lt;*internal&gt;
\fi
\def\nameofplainTeX{plain}
\ifx\fmtname\nameofplainTeX\else
  \expandafter\begingroup
\fi
%&lt;/internal&gt;</pre>
Back with the special ‘internal’ guards, the <code>\iffalse</code> is ended and a check is made on the current format. For LaTeX, a group needs to be begun so that DocStrip can be loaded without later problems. For plain TeX, only the extraction is going to happen, so that is not an issue.
<pre>%&lt;*install&gt;
\input docstrip.tex
\keepsilent
\askforoverwritefalse</pre>
The next section, inside ‘install’ guards, is the instructions for extracting the code out of the dtx. Later, this will also turn into a stand-alone ins file. DocStrip gets loaded, then we tell it to do its job without asking for any conformation or printing too much stuff.
<pre>\preamble
----------------------------------------------------------------
demopkg --- description text
E-mail: you@your.domain
Released under the LaTeX Project Public License v1.3c or later
See http://www.latex-project.org/lppl.txt
----------------------------------------------------------------

\endpreamble
\postamble

Copyright (C) 2009 by You &lt;you@your.domain&gt;

This work may be distributed and/or modified under the
conditions of the LaTeX Project Public License (LPPL), either
version 1.3c of this license or (at your option) any later
version.  The latest version of this license is in the file:

http://www.latex-project.org/lppl.txt

This work is "maintained" (as per LPPL maintenance status) by
You.

This work consists of the file  demopkg.dtx
and the derived files           demopkg.ins,
                                demopkg.pdf and
                                demopkg.sty.

\endpostamble</pre>
Some simple boiler-plate text, that DocStrip will add to the start and end of each extracted file. Of course, this can say what you like.
<pre>\usedir{tex/latex/demopkg}
\generate{
  \file{\jobname.sty}{\from{\jobname.dtx}{package}}
}</pre>
This section is the instruction to actually extract the LaTeX package file from the dtx. Each file to be extracted needs a line saying how to create it, so if there is a class to extract there would be a line for that, and so on. The <code>\usedir</code> instruction can be used to tell DocStrip how to lay files out: it is best to include it as some people use this. Normally, it will just specify <code>tex/latex/<em>&lt;package&gt;</em></code>, but might change if there are lots of files to lay out in a structured way. For example, cfg files are often put in <code>tex/latex/<em>&lt;package&gt;</em>/config</code>.
<pre>%&lt;/install&gt;
%&lt;install&gt;\endbatchfile</pre>
That ends what will get extracted into the ins file, so the install guard is closed. The second line is needed as the ins file needs to include <code>\endbatchfile</code> (for DocStrip), but we don't want the same effect when the dtx is doing the extracting.
<pre>%&lt;*internal&gt;
\usedir{source/latex/demopkg}
\generate{
  \file{\jobname.ins}{\from{\jobname.dtx}{install}}
}
\nopreamble\nopostamble
\usedir{doc/latex/demopkg}
\generate{
  \file{README.txt}{\from{\jobname.dtx}{readme}}
}
\ifx\fmtname\nameofplainTeX
  \expandafter\endbatchfile
\else
  \expandafter\endgroup
\fi
%&lt;/internal&gt;</pre>
When extracting the dtx (with TeX or LaTeX), we need to generate the ins file and the README, which is done here. The ins file is quite simple: the the same process as the sty file. However, there are a couple of points about the README. First, we don't want DocStrip to add any extra text, hence <code>\nopreamble</code> and <code>\nopostamble</code>. Second, DocStrip can only make files with extensions, so the file has to be called README.txt. (It can be renamed later: hopefully there is no loss of clarity.) If plain TeX is in use, that is the end of the processing, whereas for LaTeX the group containing DocStrip can be closed.
<pre>%&lt;*package&gt;
\NeedsTeXFormat{LaTeX2e}
\ProvidesPackage{demopkg}[2009/10/06 v1.0 description text]
%&lt;/package&gt;</pre>
Next, the fact that DocStrip can process blocks in different places can be used for the same file. This part of the package does not really need to be printed later on, and done this way the version number is included near the top of the source. Things don't have to be done this way: this section can always be left out if you like.
<pre>%&lt;*driver&gt;
\documentclass{ltxdoc}
\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage{\jobname}
\usepackage[numbered]{hypdoc}
\EnableCrossrefs
\CodelineIndex
\RecordChanges
\begin{document}
  \DocInput{\jobname.dtx}
\end{document}
%&lt;/driver&gt;</pre>
The next block is the driver: this is the information used to typeset the code and documentation. I normally load the package I'm talking about so that I can use it in the documentation, and load a few refinements (modern fonts, hyperdoc to get hyperlinks, and so on). There are a few ltxdoc-specific instructions here: they mean that we get a proper index and information linking macro use information to the code.
<pre>% \fi</pre>
This matches the <code>\iffalse</code> in the very first line of the file: it marks the beginning of material which will actually be typeset.
<pre>%
%\GetFileInfo{\jobname.sty}
%
%\title{^^A
%  \textsf{demopkg} --- description text\thanks{^^A
%    This file describes version \fileversion, last revised \filedate.^^A
%  }^^A
%}
%\author{^^A
%  You\thanks{E-mail: you@your.domain}^^A
%}
%\date{Released \filedate}
%
%\maketitle
%</pre>
Here, the title is set up and printed. A few things to notice here. By using <code>\GetFileInfo</code>, the version and date information are picked up from the package itself: no repetition of the information is needed in the dtx. Also, we can't use <code>%</code> as a comment character, and so ltxdoc sets up <code>^^A</code> to do the job instead.
<pre>%\changes{v1.0}{2009/10/06}{First public release}</pre>
General changes (not associated with any particular macro) are best listed somewhere early on. These will be used by the <code>\PrintChanges</code> macro to provide users with a change log.
<pre>%
%\DescribeMacro{\examplemacro}
% Some text about an example macro called \cs{examplemacro}, which
% might have an optional argument \oarg{arg1} and mandatory one
% \marg{arg2}.
%</pre>
This is where the documentation goes. I've included an example macro with a couple of
arguments as reminders of the syntax.
<pre>%\StopEventually{^^A
%  \PrintChanges
%  \PrintIndex
%}
%</pre>
This macro marks the end of the user part of the documentation. The two functions in the argument
will be used either here (if the code is not typeset) or after the code (if it is typeset). As the dtx file is now,
the code will print. However, in the next blog post I'll talk about printing only the documentation and
missing the code out.
<pre>%    \begin{macrocode}
%&lt;*package&gt;
%    \end{macrocode}</pre>
The lead off for the package code itself opens the guard for extracting the code. Normally, I like to have this on its own, to remind where what is going on.
<!-- {% raw %} -->
<pre>%
%\begin{macro}{\examplemacro}
%\changes{v1.0}{2009/10/06}{Some change from the previous version}
%    \begin{macrocode}
\newcommand*\examplemacro[2][]{%
  Some code here, probably
}
%    \end{macrocode}
%\end{macro}
%</pre>
<!-- {% endraw %} -->
Here we have some code: separated out using the macrocode environment. As I described in the last post, the <code>\begin{macro}</code> … <code>\end{macro}</code> block indicates that this is where <code>\examplemacro</code> is defined: indexing needs to know this. The <code>\changes</code> given in the code block only get printed if the code is typeset. They are therefore best used for low-level information, rather than usage changes that users need to know about.
<pre>%    \begin{macrocode}
%&lt;/package&gt;
%    \end{macrocode}
%\Finale</pre>
The last part of the file: close the guard for the code, and call <code>\Finale</code>. This runs anything delayed from the earlier <code>\StopEventually</code>, so in this case the index will get printed here if the code is typeset.
