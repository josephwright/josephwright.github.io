---
id: 1333
title: 'arara: Making LaTeX files your way'
date: 2012-04-24T21:17:49+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1333
permalink: /2012/04/24/arara-making-latex-files-your-way/
categories:
  - General
tags:
  - arara
---
<p>Building a LaTeX source of any complexity means doing more than a single LaTeX run, for example requiring BibTeX or MakeIndex runs along with multiple LaTeX passes. There are several ways to automate this: you can build your own script or use auto-build tools such as <a href="http://www.phys.psu.edu/~collins/software/latexmk-jcc/">latexmk</a> or <a href="https://launchpad.net/rubber">Rubber</a>. These tools work by checking for changes in the various auxiliary files that LaTeX creates, so they can work out how many runs are needed. However, a lot of users prefer to retain control of building, and so do the various steps by hand. There is now a tool that leaves the user in control but which helps to automate building: <a href="https://github.com/cereda/arara">arara</a> by <a href="http://tex.stackexchange.com/users/3094/paulo-cereda">Paulo Cereda</a>. Arara is a Java-based system, which will automatically run the tools you ask it to based on comments in your source. It's also up to you to set up the tools you want: you can already <a href="https://github.com/marcodaniel/arara/tree/master/rules/plain">get quite a selection</a> thanks to <a href="http://tex.stackexchange.com/users/5239/marco-daniel">Marco Daniel</a>. How does this work then? In your LaTeX source, you have something like</p>

<pre>% arara: pdflatex
% arara: bibtex
% arara: pdflatex
% arara: pdflatex</pre>

<p>which as you might guess does the classic pdfLaTeX, BibTeX, pdfLaTeX, pdfLaTeX cycle (assuming you have created rules called</p>

<p><code>pdflatex</code> and <code>bibtex</code>). Life gets a bit more interesting when you start adding options to the different tools. For example, if you want to allow shell escape for just one file, you can do</p>

<pre>% arara: pdflatex: { shell : yes }
% arara: bibtex
% arara: pdflatex: { shell : yes }
% arara: pdflatex: { shell : yes }</pre>

<p>without needing to leave it on for everything. As you can edit the rules easily, it's very easy to add specialist options for the way</p>

<p><em>you</em> work, even if no-one else would ever be interested in them. It also makes it easy to run both pdfLaTeX and traditional dvips routes without having to alter the settings in your editor: just add the appropriate arara rules to your files, and the correct route is chosen automatically. Arara is very much in development at the moment, and that means there are a few rough edges. For example, you have to set up the right bits and pieces yourself: no installer just yet! However, it looks like a great way to have control over exactly what gets run without needing to script everything yourself.</p>
