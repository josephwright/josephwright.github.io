---
title: Low-level definition changes
layout: post
permalink: /2009/02/17/low-level-definition-changes/
categories:
  - LaTeX3
---
The current [LaTeX3](https://www.latex-project.org/latex3.html) refactor is examining a number of different parts of the LaTeX3 code base. Although the code ideas work well, in general, they've built up over some time and this means that not everything is consistent. At the same time, issues that have happened with LaTeX2ε are helping to inform ideas about what is needed for LaTeX as a programming language.

Two somewhat related issues to do with definition are currently being revised. The first concerns the TeX `\long` definition concept. At a user level, restricting function input so that an error occurs with a `\par` token is normally a good idea. Often, trying to send a `\par` token to a user function indicates that closing brace, which is not a good thing. However, for a programming language (expl3) things are different. The general programming tools in expl3 need to handle any input, with validation on the boundary between user and internal functions. For that reason, many of the functions provided by expl3 are `\long`. As part of the refactor, the standard method for creating new functions will be to make them` \long`: you have to specifically ask for restricted arguments. In many ways, this is the same as the `\newcommand` _versus_ `\newcommand*` situation in LaTeX2ε: a bit more typing is needed if you don't want to accept paragraphs.

One area that is being improved is the “module prefixes”. A lot of these are quite logical (for example, everything to do with comma-separated lists starts `\clist`), but some of the more basic parts of the language are more variable. The basic TeX definition primitives `\let`, `\def` and `\edef` were originally simply given argument specifiers becoming `\let:NwN`, `\def:Npn` and `\def:Npx`, respectively (and so on for related primitives). None of these names have any module name at all: not really good for consistency. The team are now moving to a radically different idea, dropping terms such as “let” and “def” entirely. All of the functions are given the module prefix `\cs`, and by analogy with other parts of LaTeX3, these functions can all be regarded as setting something. This leads to names such as:

- `\cs_set_eq:NwN `(`\let`)
- `\cs_set:Npn` (`\long\def`)
- `\cs_set:Npx` (`\long\edef`)
- `\cs_set_nopar:Npn` (`\def`)
- `\cs_set_protected:Npn` (`\protected\long\def`)
- `\cs_set_protected_nopar:Npn` (`\def`) (`\protected\def`)

Globally setting is simply a case of replacing `set` by `gset`:

- `\cs_gset_eq:NwN `(`\global\let`)
- `\cs_gset:Npn` (`\global``\long\def`)
- `\cs_gset:Npx` (`\global``\long\edef`)
- `\cs_gset_protected:Npn` (`\global\long\protected``\def`)
- `\cs_gset_nopar:Npn` (`\global``\def`)

For creating new functions (where a check is made first in the hash table), the `set` (or `gset`) term is replaced by `new` (or `gnew`), again following the pattern elsewhere in LaTeX3. The above is all illustrated with the basic argument specifiers `Npn` and `Npx`, but the full range of variants are of course still available. Notice how the shorter definition names are `\long`, and to get a restricted definition the `nopar` term is needed.

Overall, this seems quite a logical change for LaTeX3. As a self-consistent programming language, it all adds up (although it will take a bit of getting used to!).
