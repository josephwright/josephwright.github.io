---
title: Active characters again
layout: post
permalink: /2009/12/09/active-characters-again/
categories:
  - General
---
A while ago I wrote about [avoiding active characters](/2009/07/04/avoiding-active-characters/). There was a question on the [LaTeX3 mailing list](http://listserv.uni-heidelberg.de/cgi-bin/wa?A0=latex-l) recently, where this came up again. So I thought I'd talk about it again here.

ε-TeX provides the primitive `\scantokens`, which can be used to re-assign the category codes of (most) input. This can be used to make some tokens in the input active, and then swap them for something else. For example:

<!-- {% raw %} -->
```latex
\begingroup
  \catcode`\:=13\relax
  \gdef\example#1{%
    \begingroup
      \catcode`\:=13\relax
      \def:{[colon]}%
      \xdef\temp{\scantokens{#1}}%
    \endgroup
    \temp
  }
```
<!-- {% endraw %} -->

This will replace every ':' in #1 with '[colon]'. As this is done by the engine, it is pretty fast. With the characters only made active locally, it also looks safe. However, I've found that this does not necessarily follow. For example, in [`siunitx`](https://ctan.org/pkg/siunitx) (version 1), there is a problem using htlatex under some circumstances because both want to make `^` active in this way. The other problem is that making characters active in this way makes it impossible to 'protect' them from replacement.

The alternative is to look through the input for each ':' and replace it one at a time: this is done in [LaTeX3](https://www.latex-project.org/latex3.html) using `\tl_replace_all_in:Nnn`. At first sight, this does not look desirable as it is never going to be as fast as using TeX primitives. However, if the code is well written (and `\tl_replace_all_in:Nnn` certainly is), then there is no need to loop over every token to do the replacement. Whatever code is used for the replacement, the key advantage is that there is no chance of a clash with different packages doing the same thing. It also leaves open the possibility of protecting some tokens from being changed. So I'd always favour avoiding active characters, if at all possible.
