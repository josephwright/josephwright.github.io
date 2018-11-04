---
id: 1157
title: 'Writing a curriculum vitae in LaTeX: Part 3'
date: 2011-11-07T09:18:49+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1157
permalink: /2011/11/07/writing-a-curriculum-vitae-in-latex-part-3/
categories:
  - General
tags:
  - curriculum vitae
  - résumé
---
I work in a university, so an important part of my CV is a list of my publications. In <a title="Writing a curriculum vitae in LaTeX: Part 2" href="http://www.texdev.net/2011/11/06/writing-a-curriculum-vitae-in-latex-part-2/">part 2</a>, I described how I put together the bulk of my CV using some custom macros: here, I'll focus on publications.
<h2>BibTeX?</h2>
The obvious approach to setting up a publication list is to use a BibTeX database. I have all of my publications in one, so that does suggest itself as an easy way to go. As with the balance between pre-built styles and custom macros, I've decided that for a CV the task is sufficiently specialised that doing it by hand is actually easier. There are a few reasons.

Usually, you give your publications in date order, newest first. That won't quite come out correctly if you simply order by year, so using BibTeX it's best to <code>\nocite</code> the keys in the order you want. No big deal, but it does mean you can't just dump them all in one go.

There are a couple of style differences between what I want in my CV and what I'd usually use in a publication. We chemists don't normally include article titles in citations, but for a CV it makes sense to add these. At the same time, I like to add hyperlinks to my publications in my CV using the <a href="http://www.doi.org">DOI </a>system. These can both be added to a standard BibTeX style (indeed, my own <a href="http://ctan.org/pkg/biblatex-chem">biblatex-chem</a> style already has a switch for titles), but of course it's another thing to sort out.

The inclusion of article titles brings me to perhaps the biggest reason that I'm not using BibTeX for my CV. Chemistry titles tend to contain lots of awkward material, such as formulae, which are hard to line break well. So there is a bit of work to do by hand to get things looking right. If I only ever used the publication list in my CV, with one set of formatting rules, then that would be fine. However, I use it in a few ways, and so manually adjusting line breaks <em>via</em> BibTeX is more awkward than simply including the text directly.
<h2>A little structure</h2>
While usually my publication list is part of my CV, I sometimes need it as a stand-alone document. So I have the list itself as a separate file, and <code>\input</code> it into the main CV source. So all I have to do for a stand-alone list of publications is write a short wrapper around the list (again as a separate file).

Whether you use BibTeX or not, you'll need to do is set up a reverse-enumerated environment, so that the most recent publication has the highest number. I do that using the <a href="http://ctan.org/pkg/etaremune">etaremune</a> package, which provides a suitable environment. The package needs to know how many items to enumerate, so either two LaTeX runs or a known starting value are needed. As I work by hand, I go with the latter approach
<pre>\begin{etaremune}[start  = 45] % Update when you add a publication
   ...
\end{etaremune}</pre>
It's then just a question of filling in the items. I use a couple of custom macros for this. First, to let me quickly wrap up each entire item in a hyperlink, I define
<pre>\newcommand*{\paper}[2]{%
  % Standard style
  \item \href{http://dx.doi.org/#1}{\ignorespaces#2\unskip.}
  % Including DOI
  %\item \href{http://dx.doi.org/#1}
  %  {\ignorespaces#2\unskip.\\\textsc{doi}: \texttt{#1}}
}</pre>
which takes the text as <code>#1</code> and the DOI as <code>#2</code>. As you can see from the comments, this lets me quickly decide whether I want to include the DOI in the printed output or to just use it to create a link.

The second custom macro is one for the paper title
<pre>\newcommand*{\papertitle}[1]{%
  \begingroup
    \addfontfeature{Numbers = Lining}%
    \emph{#1}%
  \endgroup
}</pre>
There are a couple of reasons for having a macro here. The first is that lining numbers seem to work better in chemical formulae than lower case ones do: of course this is my opinion! The second reason is that it makes it easy to quickly omit the title entirely if I need a short version of the publication list.
<h2>Putting it all together</h2>
I've covered a few different ideas for creating a CV in LaTeX. Each one is I hope pretty simple, and as I've said most people want a CV that's in a style they have chosen. But it's always nice to have something complete to start from. So in the final part of this short series, I'll put the various ideas together into an example.