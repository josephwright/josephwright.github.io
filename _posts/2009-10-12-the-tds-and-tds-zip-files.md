---
title: The TDS and TDS zip files
layout: post
permalink: /2009/10/12/the-tds-and-tds-zip-files/
categories:
  - General
tags:
  - DTX
  - TDS
---
In my post about [working with dtx files](/2009/10/11/working-with-dtx-files/), I made the somewhat throw-away statement

> The idea of a TDS-ready zip is also popular …

I've been pulled up on that by e-mail, so I  thought I'd consider this a bit more before looking at automating working with dtx sources.

First, what does ‘TDS’ mean? The short answer is _TeX Directory Structure_, but that does not really help. The idea of the TDS is to have a standard layout for the location of TeX files, so for example LaTeX .sty files go inside `tex/latex/` (or more likely `tex/latex/_&lt;package&gt;_/`), while BibTeX style files (.bst) go inside `bibtex/bst`.

That's important as both [TeX Live](https://tug.org/texlive/) and [MiKTeX](https://www.miktex.org) use a database to locate files, and only scan the ‘correct’ parts of the TeX installation when building the database. So if you do a local file installation and put the file in the wrong place TeX won't find it. The result is that you need to lay things out properly if you're installing TeX files, which can be confusing if you're not familiar with the idea.

The TDS zip idea is very simple: rather than having just the source files in a zip, set up the documentation, extracted package, source and so on in the correct layout. The end user can then just unzip the TDS zip inside their local TeX directory to install a package (of course, they'll still need to run `texhash`). As a package author, sending a user a file they can just unzip and use is much faster in the long run than sending them a bunch of files with a list of installation instructions on where everything needs to go.

The downside of the system is that the TDS zip has to be built in the first place, by the package author. With a batch script or Makefile for doing releases, that's not an issue, but it is if everything is being done by hand. Mistakes can be a problem (even with a script, if you get it wrong!).

One argument against needing TDS zips is that both TeX Live and MiKTeX update very regularly, and so it's easy to install a package from [CTAN](https://www.ctan.org) using the package manager of your TeX system. However, not everyone is using a burning edge system. Many Linux systems are still on TeX Live 2007, and on multi-user systems the TeX system is probably fixed by the administrator.  So doing local installations is still a reality for a lot of people.

Over all, I think the idea has merit, but as a package author you do need to put in some effort to get things ‘right’. I'll be talking about some scripting in my next post, and hopefully the ideas there will show how things can be done reliably. The overall aim is to make life easier for non-experts, and if that means a bit more effort for the more experienced TeX users then I think the trade-off is not too bad. I don't expect everyone to agree with me!
