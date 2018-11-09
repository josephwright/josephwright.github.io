---
title: Units outside of \SI and \si
layout: post
permalink: /2009/01/14/units-outside-of-si-and-si/
categories:
  - Packages
  - siunitx
---
A recent discussion on the [LaTeX Community](https://latex.org/forum/) forums has raised the point that [`siunitx`](https://ctan.org/pkg/siunitx) currently defines a lot of short unit macros outside of the scope of the `\SI` and `\si` macros.  I did this to match the functionality of the [`unitsdef`](https://ctan.org/pkg/unitsdef) package, but I'm thinking of revising this for version 2. There will be an option to get [`unitsdef`](https://ctan.org/pkg/unitsdef)-like behaviour (which I don't think is actually very good).

Looking further ahead, I suspect I'll be more definite about things when I write a [LaTeX3](https://www.latex-project.org/latex3.html) version of `siunitx`. There, backward-compatibility is not an issue, so I'll be free to do what is most sensible for the long term.
