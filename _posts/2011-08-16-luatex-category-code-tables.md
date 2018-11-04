---
id: 1082
title: LuaTeX category code tables
date: 2011-08-16T09:07:27+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1082
permalink: /2011/08/16/luatex-category-code-tables/
categories:
  - General
tags:
  - catcode
  - LuaTeX
---
There are lots of very clever ideas in <a href="http://www.luatex.org/">LuaTeX</a>, and it's easy to miss some of the good stuff there is. One that many people might miss is category code tables. As any TeX programmer rapidly becomes aware, category codes are central to TeX, and the construction
<pre>\catcode`\&lt;char&gt; = &lt;number&gt;\relax</pre>
is one you soon get used to. The problem comes when several people start altering the codes: there is no easy way to get back to a known position.

A good illustration of this is verbatim material. The way that something like LaTeX's \verb macro works is by setting the category code for all of the ‘special’ characters to ‘other’:
<pre>\let\do\@makeother
\dospecials</pre>
where both <code>\@makeother</code> and <code>\dospecials</code> are provided by the LaTeX kernel. That works because <code>\dospecials</code> is defined as
<pre>\do \ \do \\\do \{\do \}\do \$\do \&amp;\do \#\do \^\do \_\do \%\do \~</pre>
and so maps the function <code>\@makeother</code> to all of the ‘special’ characters. Using that, a (simplified) verbatim command looks like
<pre>\makeatletter
\newcommand*\stdverb{%
  \begingroup
    \let\do\@makeother
    \dospecials
    \@stdverb
}
\newcommand*\@stdverb[1]{%
  \catcode`#1=\active
  \lccode`\~=`#1%
  \lowercase{\let~}\endgroup
  \ttfamily
}
\makeatother</pre>
In most cases, this works fine. However, if someone makes another character ‘special’ then things go wrong:
<pre>\catcode`\+=\active
\newcommand+{oops}
\stdverb=#{+=</pre>
Of course, you could loop over <em>every</em> character, which would be slow for 8-bit input but with UTF-8 input that becomes impractical. Of course, you could add each active character to <code>\dospecials</code>, but this is dependent on everyone sticking to good practice.

This is where category code table come in. These are pre-set lists of category codes, which can be applied in one go. Heiko Oberdiek's <a href="http://www.ctan.org/pkg/luatex-pkg" title="Basic definitions for LuaTeX"><code>luatex</code></a> package provides a LaTeX interface for these, meaning we can do:
<pre>\usepackage{luatex}
\makeatletter
\newcommand*\luaverb{%
  \begingroup
    \BeginCatcodeRegime\CatcodeTableOther
    \@stdverb
}
\makeatother</pre>
(reusing the same internal macro as before). now trying
<pre>\catcode`\+=\active
\newcommand+{oops}
\luaverb=#{+=</pre>
works as expected, as all of the category codes change in one go. Simple, clear and effective!