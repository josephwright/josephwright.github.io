---
id: 102
title: Units outside of \SI and \si
date: 2009-01-14T20:12:08+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=102
permalink: /2009/01/14/units-outside-of-si-and-si/
categories:
  - Packages
  - siunitx
---
A recent discussion on the <a href="http://latex-community.org/">LaTeX Community</a> forums has raised the point that <a href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> currently defines a lot of short unit macros outside of the scope of the \SI and \si macros.  I did this to match the functionality of the <a href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=unitsdef">unitsdef</a> package, but I'm thinking of revising this for <a href="http://siunitx.berlios.de">version 2</a>. My plan is to change the default behaviour so that these macros will only work inside <code>\SI</code> and <code>\si</code> (plus the <code>s</code> column). There will be an option to get <a title="Typesetting units in LaTeX" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=unitsdef">unitsdef</a>-like behaviour (which I don't think is actually very good).

Looking further ahead, I suspect I'll be more definite about things when I write a <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a> version of siunitx. There, backward-compatiblity is not an issue, so I'll be free to do what is most sensible for the long term.