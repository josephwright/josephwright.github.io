---
id: 1338
title: Text blocks on both sides of the header
date: 2012-04-26T08:37:29+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1338
permalink: /2012/04/26/text-blocks-on-both-sides-of-the-header/
categories:
  - General
---
A while ago, I wrote a <a title="Writing a curriculum vitae in LaTeX: Part 1" href="http://www.texdev.net/2011/11/05/writing-a-curriculum-vitae-in-latex-part-1/">short series on creating a CV in LaTeX</a>. I've made a few adjustments recently, both to my CV and my letter of application, and one issue came up in both of them: putting text on both sides of the header.

For my CV, I wanted to split the address block I put at the top into two parts: address on one side, phone numbers on the other. The easiest way to do that turns out to be a tabular
<pre>
\noindent
\begin{tabular}{@{}p{0.5\textwidth}@{}p{0.5\textwidth}@{}}
  \raggedright
  \textbf{Name} \\
  Address Line 1\\
  Address Line 2\\
  ...
  &
  \raggedleft
  \null               \par
  Tel.\ xxx xxxxxx    \\
  Mobile yyy yyy yyyy \\
  someone@some.domain
\end{tabular}
</pre>
There are a few things to notice here. First, I've made the table columns take up all of the width of the page by using <code>@{}</code> to remove any inter-column space, then divided the available space up exactly. I've used <code>\raggedleft</code> to push the phone numbers to the right-hand margin, and have forced a blank line at the top of the phone number block so the name comes above everything.

For my letter, I wanted the two blocks again but needed both to be ragged right and with the right-hand one pushed to the right margin. That needs a couple of tables
<pre>
  \begin{tabular}{@{}p{0.5\textwidth}@{}p{0.5\textwidth}@{}}
    \raggedright
    \toname
    \\
    \toaddress
    \hfil
  &
    \raggedleft
    \begin{tabular}[t]{l@{}}
      \ignorespaces
      \fromaddress
      \\[1 em]%
      \@date
    \end{tabular}
  \end{tabular}
</pre>
(This is an adjustment of the standard <code>letter</code> class, hence the various storage macros.) What you'll notice here is that I've used a nested tabular purely to get the alignment right: the <code>[t]</code> argument is vital to get both blocks to line up at the top of the page.

Both of these are quite easy once you know how, but it took a while to get them spot-on!
