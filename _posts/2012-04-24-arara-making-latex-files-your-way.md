---
title: arara: Making LaTeX files your way
layout: post
permalink: /2012/04/24/arara-making-latex-files-your-way/
categories:
  - General
tags:
  - arara
---
Building a LaTeX source of any complexity means doing more than a single LaTeX run, for example requiring BibTeX or MakeIndex runs along with multiple LaTeX passes. There are several ways to automate this: you can build your own script or use auto-build tools such as [latexmk](http://www.phys.psu.edu/~collins/software/latexmk-jcc/) or [Rubber](https://launchpad.net/rubber). These tools work by checking for changes in the various auxiliary files that LaTeX creates, so they can work out how many runs are needed. However, a lot of users prefer to retain control of building, and so do the various steps by hand. There is now a tool that leaves the user in control but which helps to automate building: [arara](https://github.com/cereda/arara) by [Paulo Cereda](https://tex.stackexchange.com/users/3094/paulo-cereda). Arara is a Java-based system, which will automatically run the tools you ask it to based on comments in your source. It's also up to you to set up the tools you want: you can already [get quite a selection](https://github.com/marcodaniel/arara/tree/master/rules/plain) thanks to [Marco Daniel](https://tex.stackexchange.com/users/5239/marco-daniel). How does this work then? In your LaTeX source, you have something like

```latex
% arara: pdflatex
% arara: bibtex
% arara: pdflatex
% arara: pdflatex
```

which as you might guess does the classic pdfLaTeX, BibTeX, pdfLaTeX, pdfLaTeX cycle (assuming you have created rules called `pdflatex` and `bibtex`). Life gets a bit more interesting when you start adding options to the different tools. For example, if you want to allow shell escape for just one file, you can do

```latex
% arara: pdflatex: { shell : yes }
% arara: bibtex
% arara: pdflatex: { shell : yes }
% arara: pdflatex: { shell : yes }
```

without needing to leave it on for everything. As you can edit the rules easily, it's very easy to add specialist options for the way

_you_ work, even if no-one else would ever be interested in them. It also makes it easy to run both pdfLaTeX and traditional dvips routes without having to alter the settings in your editor: just add the appropriate arara rules to your files, and the correct route is chosen automatically. Arara is very much in development at the moment, and that means there are a few rough edges. For example, you have to set up the right bits and pieces yourself: no installer just yet! However, it looks like a great way to have control over exactly what gets run without needing to script everything yourself.
