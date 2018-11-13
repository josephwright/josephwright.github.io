---
title: siunitx version 2&#58; snapshot 3
layout: post
permalink: /2009/11/23/siunitx-version-2-snapshot-3/
categories:
  - Packages
  - siunitx
---
It's been a while since I gave an update on progress with [`siunitx`](https://ctan.org/pkg/siunitx) version 2. I've had other things on the go, but am trying to make some progress with the code as I have lots of bugs which are fixed in the new version. Since the last snapshot, I've gone back over everything and moved internally to [`expl3`](https://ctan.org/pkg/expl3) syntax. That makes my life a lot easier, as there are lots of tools available without needing to write them all for myself. It does mean that users/testers will need to have expl3 installed: you will need the most recent release, which should appear in [TeX Live](https://tug.org/texlive/) and [MiKTeX](https://www.miktex.org/) soon for online installation, or can be downloaded from [CTAN](https://www.ctan.org) (look for [expl3.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=expl3.tds.zip&amp;Search=Search)).

There are some notes and outstanding questions with the current snapshot: it is still some way from being finished. Things to be aware of or to think about:

- Places where units should be repeated are not working properly at the moment. That is the next thing I need to sort out: I'd hope it will be done soon (perhaps another snapshot in a couple of weeks)
- I'd set the defaults to use text mode for units and math mode for numbers. This may not stay that way, see for example the results for `\SI{1.23}{J.mol^{-1}.K^{-1}}`. This is because printing units literally has to do the powers in the same font as the units.
- The options system is now using the LaTeX3 l3keys module. Following the pattern that looks likely for LaTeX3 work, I've given the options names divided into words using hyphens. I hope that they make sense.
- At present, complex numbers are always printed with the complex root (i) after the number. I need an option to reverse this, but can't think of a good name.
- I've tried to simplify the various '`trapambig...`' options into a single one (`use-brackets`). I'm not sure if this will work for everyone: do people need the ability to turn bracketing on and off in a more granulated way?

For those who want to test things out, you can get:

- The source (`.dtx` file)
- [The documentation (PDF file)](/uploads/2009/11/siunitx.pdf)
- The extracted package (`.sty` file)
- [A ready-to-install (TDS) `.zip` file](/uploads/2009/11/siunitx.tds_.zip)
