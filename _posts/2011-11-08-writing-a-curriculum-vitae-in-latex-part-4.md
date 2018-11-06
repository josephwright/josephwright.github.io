---
id: 1167
title: 'Writing a curriculum vitae in LaTeX: Part 4'
date: 2011-11-08T20:31:29+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1167
permalink: /2011/11/08/writing-a-curriculum-vitae-in-latex-part-4/
categories:
  - General
tags:
  - curriculum vitae
  - résumé
---
I've looked over the last few days at some issues centring on writing a CV in LaTeX, first <a title="Writing a curriculum vitae in LaTeX: Part 1" href="http://www.texdev.net/2011/11/05/writing-a-curriculum-vitae-in-latex-part-1/">looking at the wider picture</a>, then at <a title="Writing a curriculum vitae in LaTeX: Part 2" href="http://www.texdev.net/2011/11/06/writing-a-curriculum-vitae-in-latex-part-2/">creating a CV using custom macros</a> and most recently at <a title="Writing a curriculum vitae in LaTeX: Part 3" href="http://www.texdev.net/2011/11/07/writing-a-curriculum-vitae-in-latex-part-3/">including a list of publications</a>. To round things off, I'm going to create a <a href="http://www.texdev.net/wp-content/uploads/2011/11/cv.tex">short example</a>: the source of <a href="http://www.texdev.net/wp-content/uploads/2011/11/cv.pdf">my own CV</a> cut down to a blog post. Before I do that, I'd point out that everyone's CV is different, and while my approach makes sense for me it should be seen very much as something to pick up ideas from more than any form of template.
<h2>Package loading</h2>
I'll start as before by loading the article class and setting up some fonts. To allow a bit of flexibility, here I've made LuaLaTeX optional, so that the file can be processed, for example, using <a href="http://www.tug.org/applications/tex4ht/mn.html">TeX4ht</a>. As far as possible, the look will be the same with pdfLaTeX or LuaLaTeX (as I <a title="Writing a curriculum vitae in LaTeX: Part 2" href="http://www.texdev.net/2011/11/06/writing-a-curriculum-vitae-in-latex-part-2/">said earlier</a>, I use LuaLaTeX for my CV as it makes some aspects of the real thing easier).
<pre>\documentclass[11pt]{article}

\usepackage{ifluatex}
\ifluatex
  \usepackage{fontspec}
  \setmainfont[Ligatures = TeX,Numbers = OldStyle]{TeX Gyre Pagella}
  \setsansfont[Ligatures = TeX]{TeX Gyre Adventor}
  \setmonofont[Ligatures = TeX]{Inconsolata}
\else
  \usepackage[T1]{fontenc}
  \usepackage{tgpagella}
  \usepackage{tgadventor}
  \usepackage{inconsolata}
\fi</pre>
The next phase is to load the rest of the support needed, with <a href="http://ctan.org/pkg/hyperref">hyperref</a> last as this is usually the best idea.
<pre>\usepackage{array,etaremune,geometry,fixltx2e,microtype,pifont}
\usepackage{ragged2e,titlesec,xcolor}
\usepackage{hyperref}</pre>
<h2>Appearance adjustments</h2>
Setting up hyperref is easy, so that is done next.
<pre>\hypersetup
  {
    hidelinks = true             ,
    pdfauthor = Joseph Wright    ,
    pdftitle  = Curriculum Vitae
  }</pre>
Now there is some adjustment of the appearance. The page size is adjusted, and as I described in <a title="Writing a curriculum vitae in LaTeX: Part 2" href="http://www.texdev.net/2011/11/06/writing-a-curriculum-vitae-in-latex-part-2/">part 2</a> I set up a custom appearance for sections and subsections. I also miss out page numbers (which should not really be needed in a two page CV), and alter spacing a little.
<!-- {% raw %} -->
<pre>\geometry
  {
    a4paper         ,
    nohead          ,
    nofoot          ,
    hmargin = 1.5cm ,
    vmargin = 2cm
  }

\titleformat{\section}{\Large\bfseries\sffamily}{}{0 em}
  {%
    \begingroup
      \color{gray!30}%
      \titleline{\leaders\hrule height 0.6 em\hfill\kern 0 pt\relax}%
    \endgroup
    \nobreak
    \vspace{-1.2 em}%
    \nobreak
  }

\titleformat{\subsection}{\large\itshape}{}{0 em}{}

\renewcommand*\arraystretch{1.4}
\pagestyle{empty}
\frenchspacing</pre>
<!-- {% endraw %} -->
<h2>Specialist macros</h2>
Now comes some custom code, first for publications as I described in <a title="Writing a curriculum vitae in LaTeX: Part 3" href="http://www.texdev.net/2011/11/07/writing-a-curriculum-vitae-in-latex-part-3/">part 3</a>.
<!-- {% raw %} -->
<pre>\newcommand*{\paper}[2]
  {\item \href{http://dx.doi.org/#1}{\ignorespaces#2\unskip.}}
\newcommand*{\papertitle}[1]
  {%
    \begingroup
      \ifluatex
        \addfontfeature{Numbers = Lining}%
      \fi
      \emph{#1}%
    \endgroup
  }</pre>
<!-- {% endraw %} -->
Next is the set up for the tabular nature of the CV. The text used here sets the width of the left-hand column, so may need to be adjusted to suite whatever is the widest thing you actually use!
<!-- {% raw %} -->
<pre>\newlength{\sidewidth}
\newlength{\mainwidth}
\AtBeginDocument
  {%
    \settowidth{\sidewidth}{\textbf{Professional bodies}\hspace{0.75 em}}%
    \setlength{\mainwidth}{\dimexpr\linewidth - \sidewidth\relax}%
  }</pre>
<!-- {% endraw %} -->
Finally for the preamble, the macros which actually go into the body of the CV
<!-- {% raw %} -->.
<pre>\newcommand*{\headline}[1]
  {%
    \hbox{%
      \llap{\ding{72}\hspace*{0.2 em}}%
      \textbf{#1}%
    }%
  }
\newenvironment{CVtable}
  {%
    \begin{tabular}
      {@{}&gt;{\bfseries}p{\sidewidth}@{}&gt;{\RaggedRight}p{\mainwidth}@{}}%
  }
  {\end{tabular}}</pre>
<!-- {% endraw %} -->
<h2>The document body</h2>
There is not so much you can say about the body of the CV! As described before, I start of with some general contact details.
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
\end{raggedleft}

\begin{center}
  \Huge\bfseries\sffamily
  Joseph Alexander Wright
\end{center}</pre>
The first of several sections. Here, I've taken one which also has subsections, which work in the normal way.
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
\end{CVtable}

\dots</pre>
Several more sections would now follow, but I'll leave this to the imagination.
<pre>\section{Academic history}

\dots</pre>
I find that it's best to start a publication list on a new page, as I have quite a lot. In the UK, this list does not count as part of the general CV, so is allowed to go beyond two pages. As I said in <a title="Writing a curriculum vitae in LaTeX: Part 3" href="http://www.texdev.net/2011/11/07/writing-a-curriculum-vitae-in-latex-part-3/">part 3 of the series</a>, it's often useful to have this list as a separate file.
<pre>\newpage

\section{List of Publications}

\begin{etaremune}[start = 45] % Remember to adjust this
  \paper{10.1021/ja2087536}{
    \papertitle{Paramagnetic Bridging Hydrides of Relevance to Catalytic
    Hydrogen Evolution at Metallosulfur Centers}, A.~Jablonskyt{\.e},
    J.\,A.~Wright, S.\,A.~Fairhurst, J.\,N.\,T.~Peck, S.\,K.~Ibrahim,
    V.\,S.~Oganesyan, and C.\,J.~Pickett, \emph{J.~Am. Chem. Soc.},
    in press
  }

  \paper{10.1039/c1cc11320h}{
    \papertitle{The role of CN and CO ligands in the vibrational relaxation
    dynamics of model compounds of the [FeFe]-\break hydrogenase enzyme},
    S.~Kaziannis, J.\,A.~Wright, M.~Candelaresi, R.~Kania, G.\,M.~Greetham,
    A.\,W.~Parker, C.\,J.~Pickett and N.\,T.~Hunt
    \emph{Phys. Chem. Chem. Phys.}, 2011, \textbf{13}, 10295--10305
  }

\end{etaremune}

\dots

\end{document}
</pre>
