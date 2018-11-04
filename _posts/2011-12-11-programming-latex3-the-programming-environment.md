---
id: 1206
title: 'Programming LaTeX3: The programming environment'
date: 2011-12-11T18:01:02+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1206
permalink: /2011/12/11/programming-latex3-the-programming-environment/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the <a title="Programming LaTeX3: Background" href="http://www.texdev.net/2011/12/07/programming-latex3-background/">previous post,</a> I mentioned that programming LaTeX3 today really means programming using LaTeX3 ideas but on top of LaTeX2e. To do that, we are going to need to load the appropriate code, and then access the LaTeX3 programming environment. The exact detail depends on whether we are programming in the preamble of a LaTeX document or creating a package. I'll look at both of these before taking a closer look at the LaTeX3 programming environment in general.  What you should notice is that the use of a separate programming environment very much separates out the process of creating code from creating documents: that is quite deliberate and is something that we'll see again in the series.
<h2>In the preamble of a document</h2>
The LaTeX3 programming code usable with LaTeX2e is available as a package called expl3 (which for various reasons is distributed as part of <a href="http://ctan.org/pkg/l3kernel">l3kernel</a>). This is loaded in the usual way
<pre>\documentclass{article}
\usepackage{expl3}</pre>
That loads the code, but does not get us into the programming environment. To do that, we need to use a couple of new macros
<pre>\ExplSyntaxOn
% Code goes here
\ExplSyntaxOff</pre>
In some ways, this is similar to the LaTeX2e <code>\makeatletter</code> … <code>\makeatother</code> idea, but as we'll see it's a bit more advanced.
<h2>In a LaTeX2e package</h2>
In exactly the same way as in a document, the first stage in using LaTeX3 programming in a package is to load the code.
<pre>\RequirePackage{expl3}</pre>
Once again, that loads the code but does not switch the syntax on. We could use <code>\ExplSyntaxOn</code> here, but for packages a more flexible alternative is to declare the package as being LaTeX3-based:
<pre>\ProvidesExplPackage
  {mypkg}               % Package name
  {2011-12-11}          % Release date
  {1.0}                 % Release version
  {Some things I wrote} % Description</pre>
This is a special version of the standard <code>\ProvidesPackage</code> macro, which will automatically turn on LaTeX3 programming syntax and more importantly turn it off at the end of the package. It also deals properly with nested package loading, and so is the recommended way to use LaTeX3 syntax inside LaTeX2e packages.
<h2>The coding environment</h2>
Whether you're using LaTeX3 syntax in a document or a package, the basic ideas are the same. The first thing to notice is that white space (spaces, tabs and new lines) are ignored inside the programming environment. This means we can use it to lay out our code more clearly, but you might wonder how to actually include a space. This is handled by defining <code>~</code> as a ‘normal’ space, rather than as the usual non-breaking version.

The programming environment also makes it possible to use <code>:</code> and <code>_</code> inside the names of commands, which are more formally called <em>control sequences</em>. TeX decides what is a valid control sequence name based on something called the <em>category code</em> of each character. I'll be explaining more about category code as we go along, but for the moment the key is to understand that that a control sequence is <code>\</code> followed either by exactly one non-‘letter’ or by one or more ‘letters’. Inside the code environment <code>:</code> and <code>_</code> are treated as letters by TeX: this is the same idea as using <code>@</code> as an extra ‘letter’ in LaTeX2e code.

Not only are <code>:</code> and <code>_</code> available for use in control sequences but they are required by the conventions of LaTeX3 programming. In contrast to LaTeX2e's sometimes haphazard use of <code>@</code> in names, there are guidelines for applying both <code>:</code> and <code>_</code> in LaTeX3 names. Rather than give a formal list now, I'll bring in the system in the next couple of posts using some examples.

One difference between programming in a document and in a package is the status of <code>@</code>. LaTeX2e automatically makes it a letter in package code, but in a document this does not happen. LaTeX3 does not assign any special meaning to <code>@</code>, and so these difference are not affected by loading LaTeX3 support.
<h2>A standard document</h2>
As we'll be needing the basics here for everything from now on, I'll assume that you are using a short testing document for LaTeX3 programming:
<pre>\documentclass{article}
\usepackage{expl3}
\ExplSyntaxOn
% Code will go here
\ExplSyntaxOff
\begin{document}
\end{document}</pre>