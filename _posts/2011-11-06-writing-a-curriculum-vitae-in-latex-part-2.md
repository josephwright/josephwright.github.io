---
id: 1142
title: 'Writing a curriculum vitae in LaTeX: Part 2'
date: 2011-11-06T12:08:54+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1142
permalink: /2011/11/06/writing-a-curriculum-vitae-in-latex-part-2/
categories:
  - General
tags:
  - curriculum vitae
  - résumé
---
In <a title="Writing a curriculum vitae in LaTeX: Part 1" href="http://www.texdev.net/2011/11/05/writing-a-curriculum-vitae-in-latex-part-1/">part 1</a>, I looked at some general ideas about writing CVs, and said that my approach is to ‘roll my own’ format based on the standard article class. Here, I want to look at the process in a bit more detail. Most of this is about using LaTeX, and so the ideas I use apply to many other cases.

I make use of quite a few packages to get the appearance as I want. Rather than list all of them at once, I'll take about the effects I'm aiming for, and include the package names as I go.
<h2>Setting up the appearance</h2>
Starting from the article class, the first thing to address is the overall appearance of the CV. The standard Computers Modern font is well designed, but I guess says ‘LaTeX’ in a may that many people don't want for a CV. With the availability of <a href="http://tug.org/xetex">XeTeX</a> and <a href="http://www.luatex.org/">LuaTeX</a>, using system fonts is easy (using <a href="http://ctan.org/pkg/fontspec">fontspec</a>, of course), and that's particularly useful if like me you have some non-Latin characters that you'd like to include in the CV but keep visually ‘matching’ everything else.  For me, LuaTeX turns out to be a better choice than XeTeX (I want fully-functional microtypography as it helps with typesetting chemical names), so my CV starts off with
<pre>% !TeX program = LuaLaTeX
\documentclass[11pt,draft]{article}

% Font set up
\usepackage{fontspec}
\setmainfont[Ligatures = TeX,Numbers = OldStyle]{TeX Gyre Pagella}
\setsansfont[Ligatures = TeX]{TeX Gyre Adventor}
\setmonofont[Ligatures = TeX]{Inconsolata}</pre>
Here, as well as loading the fonts I like, I've set up to use lower case (old style) numbers as recommend by <a href="http://www.amazon.com/Elements-Typographic-Style-Robert-Bringhurst/dp/0881792063">Bringhurst</a>. I've also included a <a title="TeXworks ‘magic comments’" href="http://www.texdev.net/2011/03/24/texworks-magic-comments/">‘magic’ comment</a> to let my <a href="http://www.texdev.net/?s=texworks">editor</a> know to use LuaLaTeX. You might wonder about the <code>draft</code> option: I'll come back to that later.

As I say, I want microtypography set up, so do
<pre>\usepackage[final]{microtype}</pre>
(Using the <code>final</code> option here will override the <code>draft</code> one set for the document class.)

That sets up the fonts, but what about page layout? Well, the standard here is to use the <a href="http://ctan.org/pkg/geometry">geometry</a> package
<pre>\usepackage[a4paper,nohead,nofoot,hmargin=1.5cm,vmargin=2cm]{geometry}</pre>
I have pretty small margins, as for a CV this seems to make the most sense. I'm also not going to use a header or footer (so set <code>\pagestyle{empty}</code>), and so remove the space normally reserved for those.
<h2>Hyperlinks</h2>
Before looking at the content of the CV, I'll mention hyperlinks as these come up throughout. My CV usually gets sent electronically, and I want to be able to include links for my e-mail address and publications. So I have
<pre>\usepackage[final]{hyperref}

\hypersetup
  {
    hidelinks = true ,
    pdfauthor = Joseph Wright ,
    pdftitle = Curriculum Vitae
  }</pre>
at the end of my package-loading section. The <a href="http://ctan.org/pkg/hyperref">hyperref</a> package deals with the links, while the set up makes them blend in to the text and adds my name to the PDF information.
<h2>Lead-off: the address block</h2>
A very common way to start a CV is with basic contact details: what I'm going to call an ‘address block’. I do this very simply
<pre>\begin{document}

% Title block
\begin{raggedleft}
  \textbf{Joseph Wright}    \\
  School of Chemistry       \\
  University of East Anglia \\
  Norwich NR4 7TJ           \\
  Tel.: 01603 592902        \\
  Mobile: 0797 414 8180     \\
  \href{mailto:joseph.wright@uea.ac.uk}
    {\texttt{joseph.wright@uea.ac.uk}} \\
\end{raggedleft}</pre>
This therefore sits at the top of the first page, and comes out (to my mind) in a very pleasing style.

Also as part of the lead-off, it's normal to have your name (<em>never</em> ‘Curriculum Vitae’), which again I do in a very straightforward way
<pre>\begin{center}
  \Huge\bfseries\sffamily
  Joseph Alexander Wright
\end{center}</pre>
<h2>Sections and subsections</h2>
A CV needs several sections, for example ‘Employment history’, ‘Skills’ and so on. The standard LaTeX <code>\section</code> is the best choice of logical mark up for these, but the appearance is going to be wrong without adjustment. Taking some inspiration from the <a href="http://ctan.org/pkg/curve">CurVe</a> class, and using the abilities of <a href="http://ctan.org/pkg/titlesec">titlesec</a> and <a href="http://ctan.org/pkg/xcolor">xcolor</a>, the output can be customised to give something much more pleasing for a CV. I use
<pre>% Create some nice looking section dividers without too much fuss
\titleformat\section{\Large\bfseries\sffamily}{}{0 em}
  {%
    % This is put in _before_ the text so that an overlap is possible
    \begingroup
      \color{gray!30}%
      \titleline{\leaders\hrule height 0.6 em\hfill\kern 0 pt\relax}%
    \endgroup
    \nobreak
    \vspace{-1.2 em}%
    \nobreak
  }</pre>
which inserts a grey bar across the page, and places the name of the section (with no number) partially overlapping the bar.

For subsections, I go for a much lower visual impact
<pre>\titleformat{\subsection}{\large\itshape}{}{0 em}{}</pre>
which is enough to make them stand out from the body text, but keeps things flowing.
<h2>The main body: lots of tables</h2>
The normal layout for the body of a CV is to use something based on a table, with ‘entries’ on the left and ‘information’ on the right. This can be done in lots of ways, but the approach I take is to set up a fixed column width in the preamble, then apply this to all of the CV. That requires a bit of set up
<pre>% Semi-automatically set up the table width
\newlength\sidewidth
\newlength\mainwidth
\AtBeginDocument{%
  \settowidth\sidewidth{\textbf{Professional bodies}\hspace{0.75 em}}%
  \setlength\mainwidth{\dimexpr\linewidth - \sidewidth\relax}%
}</pre>
Here, I'm setting two lengths to control the tables, with the only hard-coded part being the text I use to set the left-hand side width. I use the longest entry I'm going to use: in my case this is ‘Professional bodies’.

I then need the tables themselves. As they are all the same, it makes sense to set them up as a new kind of environment
<pre>\newenvironment{CVtable}
  {%
    \begin{tabular}
      {@{}&gt;{\bfseries}p{\sidewidth}@{}&gt;{\RaggedRight}p{\mainwidth}@{}}%
  }
  {\end{tabular}}</pre>
(this uses the <a href="http://ctan.org/pkg/array">array</a> package). I also <code>\renewcommand*\arraystretch{1.4}</code>, as this spreads the tables out a bit and I think makes things look less crowded.

The new environment is then used for each (sub)section, and contains the body of the CV, for example
<pre>\section{Employment history}

\subsection{Current position}

\begin{CVtable}
  2008-- &amp;
    \headline{PDRA -- University of East Anglia} \par
    Supervisor Prof.~C.~J.~Pickett \par
    Studies on [Fe]- and [FeFe]-hydrogenase active sites mimics \par
    Synthesis of novel ligands and model compounds \par
    Mechanistic studies using stopped-flow UV and IR spectroscopies
  \\
\end{CVtable}

\subsection{Previous positions}

\begin{CVtable}
  2007--2008 &amp;
    \headline{Senior Demonstrator -- University of East Anglia} \par
    Teaching degree level chemistry:
    tutorials and laboratory classes \par
    Preparation of M.~Chem.~third year practical course in
    organic chemistry
  \\

  2005--2008 &amp;
    \headline{PDRA -- University of East Anglia} \par
    Supervisor Prof.~M.~Bochmann \par
    Use of zirconium phosphonates as heterogeneous catalyst supports \par
    Synthesis of novel ligand systems for early transition metals
  \\

  2003--2004 &amp;
    \headline{PDRA -- University of Southampton} \par
    Supervisor Dr A.\,A.~Danopoulos \par
    Synthesis of novel N-heterocyclic carbene complexes \par
    Catalytic testing on novel systems
  \\
\end{CVtable}</pre>
You'll notice the <code>\headline</code> macro here: it's another formatting shortcut. It's for making effectively subsubsections within my CV table, and is defined as
<pre>\newcommand*\headline[1]{%
  \hbox{%
    \llap{\ding{72}\hspace*{0.2 em}}%
    \textbf{#1}%
  }%
}</pre>
making use of the <a href="http://ctan.org/pkg/pifont">pifont</a> package to provide a nice-looking star for each entry. You'll see in the above example that I use it for things like marking up each job I've had in the table of employment history.
<h2>Other refinements</h2>
As I mentioned in <a title="Writing a curriculum vitae in LaTeX: Part 1" href="http://www.texdev.net/2011/11/05/writing-a-curriculum-vitae-in-latex-part-1/">part 1</a>, one of the advantages of using LaTeX is that you can store information in your CV as comments. That might be as simple as commenting-out lines that you want to miss out for a particular job, but you might also want to deal with longer optional sections. The <a href="http://ctan.org/pkg/comment">comment</a> package is ideal for this, as it lets you mark up sections for inclusion or exclusion in a pretty rapid way.

I mentioned earlier that I set the <code>draft</code> option for my CV, then override it on a package-by-package basis. The reason is that this will always include bars for overfull boxes: useful as you want to check for these.

In the academic area, a list of publications is an important part of a CV (it's probably <em>the</em> most important part, actually). I've got a few things to say about that area, but this post is already long enough, so it will wait for the next part!