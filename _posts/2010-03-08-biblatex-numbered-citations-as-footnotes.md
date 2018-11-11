---
title: biblatex: numbered citations as footnotes
layout: post
permalink: /2010/03/08/biblatex-numbered-citations-as-footnotes/
categories:
  - biblatex
  - Packages
---
Most chemistry journals use numbered citation styles, with all of the references appearing at the end of the article in a References section. However, there are some that place the references at the bottom of the page they occur on, as footnotes. This is a bit more awkward to achieve than a simple section, but as [`biblatex`](https://ctan.org/pkg/biblatex) has all of the citation data available from the start of a document I thought it should be easy to do.

It turns out that `biblatex` has the very handy `\footfullcite` macro, which nearly does what is needed. This macro will print the reference as a footnote, but uses LaTeX's footnote numbering system to do this. The result is that repeating citations, compressing several citations into a range and so on is not so easy. In the end, I decided to drop Philipp Lehman (the author of `biblatex`) an e-mail for some guidance. He came back with two approaches, one for citations in the text and one for superscript citations:


<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[style=numeric-comp]{biblatex}
\bibliography{biblatex-examples}
\makeatletter

\ExecuteBibliographyOptions{citetracker,sorting=none}

\DeclareCiteCommand{\notefullcite}[\mkbibbrackets]
  {\usebibmacro{cite:init}%
   \usebibmacro{prenote}}
  {\usebibmacro{citeindex}%
   \usebibmacro{notefullcite}%
   \usebibmacro{cite:comp}}
  {}
  {\usebibmacro{cite:dump}%
   \usebibmacro{postnote}}

\newbibmacro*{notefullcite}{%
  \ifciteseen
    {}
    {\footnotetext[\thefield{labelnumber}]{%
       \usedriver{}{\thefield{entrytype}}.}}}
\DeclareCiteCommand{\superfullcite}[\cbx@superscript]%
  {\usebibmacro{cite:init}%
   \let\multicitedelim=\supercitedelim
   \iffieldundef{prenote}
     {}
     {\BibliographyWarning{Ignoring prenote argument}}%
   \iffieldundef{postnote}
     {}
     {\BibliographyWarning{Ignoring postnote argument}}}
  {\usebibmacro{citeindex}%
   \usebibmacro{superfullcite}%
   \usebibmacro{cite:comp}}
  {}
  {\usebibmacro{cite:dump}}

\newbibmacro*{superfullcite}{%
  \ifciteseen
    {}
    {\xappto\cbx@citehook{%
       \noexpand\footnotetext[\thefield{labelnumber}]{%
         \fullcite{\thefield{entrykey}}.}}}}

\newrobustcmd{\cbx@superscript}[1]{%
  \mkbibsuperscript{#1}%
  \cbx@citehook
  \global\let\cbx@citehook=\empty}
\let\cbx@citehook=\empty

\makeatother
\begin{document}

Some filler text \notefullcite{cotton}, then some more text
\notefullcite{hammond}. Perhaps some more text and the same
citation again \notefullcite{hammond}. Yet another one
\notefullcite{knuth:ct:a}. Now all again
\notefullcite{cotton,hammond,knuth:ct:a}.

Some filler text,\superfullcite{augustine} then some more
text.\superfullcite{companion} Perhaps some more text and the
same citation again.\superfullcite{companion} Yet another
one.\superfullcite{kastenholz} Now all
again.\superfullcite{augustine,companion,kastenholz}

\end{document}
```
<!-- {% endraw %} -->


I might add this to my `biblatex` styles, but I'll wait to see if Philipp puts the code or some notes into the `biblatex` core before I do. I should also point out that if you want footnote citations and other footnotes then you'll need something like the [`bigfoot`](https://ctan.org/pkg/bigfoot) package to do the job. But this is a pretty good place to start from.
