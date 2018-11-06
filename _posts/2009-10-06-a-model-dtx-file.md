---
title: A model dtx file
layout: post
permalink: /2009/10/06/a-model-dtx-file/
categories:
  - General
tags:
  - DTX
---
In my previous post, I've tried to give a very general overview of how the dtx file format comes about, from a combination of the syntax of DocStrip and ltxdoc. The problem with the bald details is that there are still lots of way to actually use the ideas to construct a dtx. So here I'm going to detail a model dtx, which is ready to be filled in with real code and documentation. The entire file is [available here as demopkg.dtx](/wp-content/uploads/2009/10/demopkg.dtx): get it now if you are impatient!

The idea of constructing a dtx file in the way I'll describe is that it lets us achieve several things in one go:

- All of the files for a package can be derived from a single source (unless you need a binary, of course).
- The README is included in the dtx, with this useful information at the start.
- The ins file is included in the dtx, so the file is self-extracting.
- Running `(pdf)tex _&lt;name&gt;_.dtx` extracts the code and associated files (ins, README, _etc_.).
- Running `(pdf)latex _&lt;name&gt;_.dtx` does the extraction then typesets the documentation. This way, the documentation always has the latest code available, and users don't need to worry about which method they use to get stuff extracted.

Most of the ideas here are not mine: Will Robertson came up with a lot of this. I'm just going to give some details of what is going on. I'm going to present the source in order, with a section of the source followed by some comments explaining what is going on. I'm going to call the demonstration package ‘demopkg’: something easy for search and replace. Where ever possible, `\jobname` is used in the source so that the file name changes automatically when moving from one package to another.

```latex
% \iffalse meta-comment
% !TEX program  = pdfLaTeX
```

The file starts off with an `\iffalse` which will mean that ltxdoc will skip all of this code when typesetting the document. I use [TeXworks](https://tug.org/texworks) as my editor, so I include the special `!TEX program` comment so that it defaults to pdfLaTeX with all of my files: this does no harm so may as well be there. The same comment is also recognised by [TeXShop](http://www.uoregon.edu/~koch/texshop/).

```latex
%&lt;*internal&gt;
\iffalse
%&lt;/internal&gt;
```

There is then a guard called ‘internal’: this is never extracted out, but lets us have an uncommented `\iffalse` in the code. which will mean that the next section will be ignored by TeX initially. The idea here is that we are going to have some text (the README), that TeX would otherwise try to typeset. We don't want that, so need to skip it at the moment.

```latex
%&lt;*readme&gt;
----------------------------------------------------------------
demopkg --- description text
E-mail: you@your.domain
Released under the LaTeX Project Public License v1.3c or later
See https://www.latex-project.org/lppl.txt
----------------------------------------------------------------

Some text about the package: probably the same as the abstract.
%&lt;/readme&gt;
```

This part is pretty obvious: the README file for the package, inside guards called ‘readme’. As you might expect, this will get extracted out later as the README file.  In the initial TeX run, this text will be skipped (because of the `\iffalse`), but when DocStrip runs it will show up (as DocStrip will ignore the `\iffalse`, which is in a different set of guards).

```latex
%&lt;*internal&gt;
\fi
\def\nameofplainTeX{plain}
\ifx\fmtname\nameofplainTeX\else
  \expandafter\begingroup
\fi
%&lt;/internal&gt;
```

Back with the special ‘internal’ guards, the `\iffalse` is ended and a check is made on the current format. For LaTeX, a group needs to be begun so that DocStrip can be loaded without later problems. For plain TeX, only the extraction is going to happen, so that is not an issue.

```latex
%&lt;*install&gt;
\input docstrip.tex
\keepsilent
\askforoverwritefalse
```

The next section, inside ‘install’ guards, is the instructions for extracting the code out of the dtx. Later, this will also turn into a stand-alone ins file. DocStrip gets loaded, then we tell it to do its job without asking for any conformation or printing too much stuff.

```latex
\preamble
----------------------------------------------------------------
demopkg --- description text
E-mail: you@your.domain
Released under the LaTeX Project Public License v1.3c or later
See https://www.latex-project.org/lppl.txt
----------------------------------------------------------------

\endpreamble
\postamble

Copyright (C) 2009 by You &lt;you@your.domain&gt;

This work may be distributed and/or modified under the
conditions of the LaTeX Project Public License (LPPL), either
version 1.3c of this license or (at your option) any later
version.  The latest version of this license is in the file:

https://www.latex-project.org/lppl.txt

This work is "maintained" (as per LPPL maintenance status) by
You.

This work consists of the file  demopkg.dtx
and the derived files           demopkg.ins,
                                demopkg.pdf and
                                demopkg.sty.

\endpostamble
```

Some simple boiler-plate text, that DocStrip will add to the start and end of each extracted file. Of course, this can say what you like.

```latex
\usedir{tex/latex/demopkg}
\generate{
  \file{\jobname.sty}{\from{\jobname.dtx}{package}}
}
```

This section is the instruction to actually extract the LaTeX package file from the dtx. Each file to be extracted needs a line saying how to create it, so if there is a class to extract there would be a line for that, and so on. The `\usedir` instruction can be used to tell DocStrip how to lay files out: it is best to include it as some people use this. Normally, it will just specify `tex/latex/_&lt;package&gt;_`, but might change if there are lots of files to lay out in a structured way. For example, cfg files are often put in `tex/latex/_&lt;package&gt;_/config`.

```latex
%&lt;/install&gt;
%&lt;install&gt;\endbatchfile
```

That ends what will get extracted into the ins file, so the install guard is closed. The second line is needed as the ins file needs to include `\endbatchfile` (for DocStrip), but we don't want the same effect when the dtx is doing the extracting.

```latex
%&lt;*internal&gt;
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
%&lt;/internal&gt;
```

When extracting the dtx (with TeX or LaTeX), we need to generate the ins file and the README, which is done here. The ins file is quite simple: the the same process as the sty file. However, there are a couple of points about the README. First, we don't want DocStrip to add any extra text, hence `\nopreamble` and `\nopostamble`. Second, DocStrip can only make files with extensions, so the file has to be called README.txt. (It can be renamed later: hopefully there is no loss of clarity.) If plain TeX is in use, that is the end of the processing, whereas for LaTeX the group containing DocStrip can be closed.

```latex
%&lt;*package&gt;
\NeedsTeXFormat{LaTeX2e}
\ProvidesPackage{demopkg}[2009/10/06 v1.0 description text]
%&lt;/package&gt;
```

Next, the fact that DocStrip can process blocks in different places can be used for the same file. This part of the package does not really need to be printed later on, and done this way the version number is included near the top of the source. Things don't have to be done this way: this section can always be left out if you like.

```latex
%&lt;*driver&gt;
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
%&lt;/driver&gt;
```

The next block is the driver: this is the information used to typeset the code and documentation. I normally load the package I'm talking about so that I can use it in the documentation, and load a few refinements (modern fonts, hyperdoc to get hyperlinks, and so on). There are a few ltxdoc-specific instructions here: they mean that we get a proper index and information linking macro use information to the code.

```latex
% \fi
```

This matches the `\iffalse` in the very first line of the file: it marks the beginning of material which will actually be typeset.

```latex
%
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
%
```

Here, the title is set up and printed. A few things to notice here. By using `\GetFileInfo`, the version and date information are picked up from the package itself: no repetition of the information is needed in the dtx. Also, we can't use `%` as a comment character, and so ltxdoc sets up `^^A` to do the job instead.

```latex
%\changes{v1.0}{2009/10/06}{First public release}
```

General changes (not associated with any particular macro) are best listed somewhere early on. These will be used by the `\PrintChanges` macro to provide users with a change log.

```latex
%
%\DescribeMacro{\examplemacro}
% Some text about an example macro called \cs{examplemacro}, which
% might have an optional argument \oarg{arg1} and mandatory one
% \marg{arg2}.
%
```

This is where the documentation goes. I've included an example macro with a couple of
arguments as reminders of the syntax.

```latex
%\StopEventually{^^A
%  \PrintChanges
%  \PrintIndex
%}
%
```

This macro marks the end of the user part of the documentation. The two functions in the argument
will be used either here (if the code is not typeset) or after the code (if it is typeset). As the dtx file is now,
the code will print. However, in the next blog post I'll talk about printing only the documentation and
missing the code out.

```latex
%    \begin{macrocode}
%&lt;*package&gt;
%    \end{macrocode}
```

The lead off for the package code itself opens the guard for extracting the code. Normally, I like to have this on its own, to remind where what is going on.

<!-- {% raw %} -->
```latex
%
%\begin{macro}{\examplemacro}
%\changes{v1.0}{2009/10/06}{Some change from the previous version}
%    \begin{macrocode}
\newcommand*\examplemacro[2][]{%
  Some code here, probably
}
%    \end{macrocode}
%\end{macro}
%
```
<!-- {% endraw %} -->

Here we have some code: separated out using the macrocode environment. As I described in the last post, the `\begin{macro}` … `\end{macro}` block indicates that this is where `\examplemacro` is defined: indexing needs to know this. The `\changes` given in the code block only get printed if the code is typeset. They are therefore best used for low-level information, rather than usage changes that users need to know about.

```latex
%    \begin{macrocode}
%&lt;/package&gt;
%    \end{macrocode}
%\Finale
```

The last part of the file: close the guard for the code, and call `\Finale`. This runs anything delayed from the earlier `\StopEventually`, so in this case the index will get printed here if the code is typeset.
