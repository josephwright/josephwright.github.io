---
id: 188
title: Low-level definition changes
date: 2009-02-17T19:41:20+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=188
permalink: /2009/02/17/low-level-definition-changes/
categories:
  - LaTeX3
---
The current <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> refactor is examining a number of different parts of the LaTeX3 code base. Although the code ideas work well, in general, they've built up over some time and this means that not everything is consistent. At the same time, issues that have happened with LaTeX2ε are helping to inform ideas about what is needed for LaTeX as a programming language.

Two somewhat related issues to do with definition are currently being revised. The first concerns the TeX <code>\long</code> definition concept. At a user level, restricting function input so that an error occurs with a <code>\par</code> token is normally a good idea. Often, trying to send a <code>\par</code> token to a user function indicates that closing brace, which is not a good thing. However, for a programming language (expl3) things are different. The general programming tools in expl3 need to handle any input, with validation on the boundary between user and internal functions. For that reason, many of the functions provided by expl3 are <code>\long</code>. As part of the refactor, the standard method for creating new functions will be to make them<code> \long</code>: you have to specifically ask for restricted arguments. In many ways, this is the same as the <code>\newcommand</code> <em>versus</em> <code>\newcommand*</code> situation in LaTeX2ε: a bit more typing is needed if you don't want to accept paragraphs.

One area that is being improved is the “module prefixes”. A lot of these are quite logical (for example, everything to do with comma-separated lists starts <code>\clist</code>), but some of the more basic parts of the language are more variable. The basic TeX definition primitives <code>\let</code>, <code>\def</code> and <code>\edef</code> were originally simply given argument specifiers becoming <code>\let:NwN</code>, <code>\def:Npn</code> and <code>\def:Npx</code>, respectively (and so on for related primitives). None of these names have any module name at all: not really good for consistency. The team are now moving to a radically different idea, dropping terms such as “let” and “def” entirely. All of the functions are given the module prefix <code>\cs</code>, and by analogy with other parts of LaTeX3, these functions can all be regarded as setting something. This leads to names such as:
<ul>
 	<li><code>\cs_set_eq:NwN </code>(<code>\let</code>)</li>
 	<li><code>\cs_set:Npn</code> (<code>\long\def</code>)</li>
 	<li><code>\cs_set:Npx</code> (<code>\long\edef</code>)</li>
 	<li><code>\cs_set_nopar:Npn</code> (<code>\def</code>)</li>
 	<li><code>\cs_set_protected:Npn</code> (<code>\protected\long\def</code>)</li>
 	<li><code>\cs_set_protected_nopar:Npn</code> (<code>\def</code>) (<code>\protected\def</code>)</li>
</ul>
Globally setting is simply a case of replacing <code>set</code> by <code>gset</code>:
<ul>
 	<li><code>\cs_gset_eq:NwN </code>(<code>\global\let</code>)</li>
 	<li><code>\cs_gset:Npn</code> (<code>\global</code><code>\long\def</code>)</li>
 	<li><code>\cs_gset:Npx</code> (<code>\global</code><code>\long\edef</code>)</li>
 	<li><code>\cs_gset_protected:Npn</code> (<code>\global\long\protected</code><code>\def</code>)</li>
 	<li><code>\cs_gset_nopar:Npn</code> (<code>\global</code><code>\def</code>)</li>
</ul>
For creating new functions (where a check is made first in the hash table), the <code>set</code> (or <code>gset</code>) term is replaced by <code>new</code> (or <code>gnew</code>), again following the pattern elsewhere in LaTeX3. The above is all illustrated with the basic argument specifiers <code>Npn</code> and <code>Npx</code>, but the full range of variants are of course still available. Notice how the shorter definition names are <code>\long</code>, and to get a restricted definition the <code>nopar</code> term is needed.

Overall, this seems quite a logical change for LaTeX3. As a self-consistent programming language, it all adds up (although it will take a bit of getting used to!).
