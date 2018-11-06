---
id: 298
title: Lua, TeX, LaTeX and ConTeXt
date: 2009-05-21T08:06:58+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=298
permalink: /2009/05/21/lua-tex-latex-and-context/
categories:
  - General
tags:
  - ConTeXt
  - LaTeX
  - LuaTeX
---
There is currently a [very active thread](http://groups.google.com/group/comp.text.tex/browse_frm/thread/d352212826544c1d/0d41be1dfa4107e8) on [comp.text.tex](http://groups.google.com/group/comp.text.tex/topics) about LuaTeX. Several related questions have come up, and it seems that some kind of summary would help me, at least.

## Why did the LuaTeX team choose Lua?

Possibly the most frequently asked question with [LuaTeX](http://www.luatex.org) is why the team behind it chose Lua, as opposed to one of the other scripting languages available. The [LuaTeX FAQ](http://www.luatex.org/faq.html) addresses this as question 1, so it's obviously important. As I understand it, they looked at a number of possible languages for extending TeX, and decided that many of the “obvious” candidates (Java, Perl, Python, Ruby, Scheme) were not suitable. Not everyone is going to agree with that assessment, and some people are bound to feel that there was not sufficient consultation.

With LuaTeX already at version 0.40, it is progressing and will deliver. So unless a team can be got together to provided an alternative scripting system, it looks like Lua is what we will get. I don't see there being enough experienced programmers with time on their hands to deliver a complete alternative at the moment.

## How does LuaTeX relate to ConTeXt and LaTeX?

LuaTeX is an “engine”, like [pdfTeX](http://www.pdftex.org) or [XeTeX](https://tug.org/xetex/). So it provides certain functions, which might or might not get used. The end-user can use them directly, but this is really not helping most people as they don't want to do this type of low-level work. So in the main it is down to either the TeX format ([ConTeXt,](http://wiki.contextgarden.net/Main_Page) [LaTeX](https://www.latex-project.org/), …) or an add on (LaTeX package,  ConTeXt module, _etc_.) to take advantage of them.

In the ConTeXt case, the entire format is being re-written as “Mark IV”, which will use a lot of Lua. This of course means things fundamentally change compared to early versions of ConTeXt, and ties it to a single engine.

In the LaTeX case, the format is written to work on plain TeX, no extensions at all. That is not about to change: essentially, LaTeX2e will _never_ be “updated” in that sense. The current [LaTeX3](https://www.latex-project.org/latex3.html) plans don't envisage requiring LuaTeX, although I'd hope that some low-level support will be included if LaTeX3 ever becomes a reality. There will, though, be LaTeX packages that use Lua: I'm sure that at some point there will be a [`fontspec`](https://ctan.org/pkg/fontspec)-like package for LuaTeX, for example.

## What is wrong with LaTeX2ε?

One issue that always comes up when future directions for TeX are discussed is whether LaTeX2ε needs to change, or whether it is okay as it is. Currently, if you know what you are doing then you can achieve a lot with LaTeX. There are a vast range of packages, and these cover very many of the things you could ever hope to do in TeX. So in a sense LaTeX works as it is. On the other hand, you have to know which packages to load, even to get some of the basics right (try making a new float type without loading any packages and using one of the base classes!). At the same time, things like UTF-8 text, system fonts and so on are not available using only the kernel.

A more fundamental issue is that LaTeX currently doesn't do enough to provide structured data, and is not a good choice for dealing with XML input. This makes it hard to get data in and out, and is closely related to the fact that there is not enough separation of appearance and structure in the kernel and in add-on packages.

Neither of these points has escaped the notice of the LaTeX team. The question is whether a successor to LaTeX2ε will appear, and if it does whether it can succeed. There is a need to start from scratch with many things, meaning that a new LaTeX simply won't work with most packages currently available. So the team have to deliver something that really works.

## How can (La)TeX  recruit new users?

One question that comes up here is what is a typical (La)TeX user anyway. Everyone has their own view on this: some people see TeX users mainly as mathematicians and physicists, other people point out that particularly with XeTeX available there is a lot of potential in the humanities.

Making life easier for new users is a priority for gaining new users. This means making it easy to install TeX (which both [TeX Live](https://www.tug.org/texlive/) and [MiKTeX](https://www.miktex.org/) do, I think), making it easier to edit TeX files (the excellent [TeXworks](http://texworks.org) helps here), and making it easier to use TeX. It is, of course, the last one that is the problem.  I think that we do need a new LaTeX as part of this. Removing the need to load a dozen packages and alter half a dozen internal macros to get reasonable output would benefit all LaTeX users. At the same time, something as simple as a generic thesis template could be made available: that would again help to “sell” LaTeX and by extension TeX as a whole.

LuaTeX has a role to play here. Using system fonts with pdfTeX is not easy, and XeTeX has helped a lot with this. LuaTeX provides this possibility and many more, and so we can hopefully look forward to not having to worry about loading system fonts at all. At the same time, it should be possible to do things similar to the current BibTeX and MakeIndex programs directly in the engine, but with full UTF-8 input. This is something that is long overdue, and again can't hurt when it comes to selling (La)TeX.
