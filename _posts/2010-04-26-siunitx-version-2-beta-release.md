---
title: siunitx version 2&#58; beta release
layout: post
permalink: /2010/04/26/siunitx-version-2-beta-release/
categories:
  - Packages
  - siunitx
---
Over the past few months I've been working a new version of [`siunitx`](https://ctan.org/pkg/siunitx) with completely re-written internals. This is now at the point where I hope that it is usable for most people, but before replaced version 1 some testing is needed. This is what this beta (testing) release is for. There are some important notes for people testing, which I'll run through below. For the impatient, you can get:

- [A ready to install `.zip` file](/wp-content/uploads/2010/04/siunitx.tds.zip)
- [The documentation](/wp-content/uploads/2010/04/siunitx.pdf)
- The source (dtx) file

## Release notes

The code used in `siunitx` relies on the [LaTeX3 Project](https://www.latex-project.org/) packages [`expl3`](https://ctan.org/pkg/expl3) and `xpackages`. You will need the latest versions of both of these to test `siunitx` 2: they can both be downloaded from [CTAN](https://www.ctan.org) or installed using the update facilities in [TeX Live](https://tug.org/texlive/) or [MiKTeX](https://www.miktex.org/).

Version 2 of `siunitx` renames most of the package options to make them more informative. The old names are available by using:

```latex
\usepackage[load-configurations = version-1]{siunitx}
```

The new option names are intended to make it easier to continue to expand `siunitx` without having completely opaque option names. At the same time, the nature of some of the options has been changed. This means that there are no longer any 'magic' keywords, which have caused confusion in the past.

There will be no significant features added to `siunitx` version 2 between the beta version and the production release (probably in June). The aim is to get the inevitable bugs in the current code found and fixed, which is best done while not making other changes.

A small number of features from version 1 of `siunitx` are not present in version 2. The features removed have never worked as well as I would like, and so I felt it was better to remove them and rework them later if needed. If this causes severe problems for users then some of these decisions may of course be reversed.

I have had a large number of feature requests for `siunitx`, and only some of these have been added to version 2 at present. This is partly as I have a limited amount of time, and need to get `siunitx` 2 to release within a reasonable time. At the same time, some of the feature requests are very specialist and I need to consider which of these fall within the scope of the package. That said, I intend to work on adding more features to `siunitx` after the full release of version 2.0. More details on this will be posted here in the future.

Feedback on any aspect of `siunitx` version 2 is very welcome: [joseph.wright@morningstar2.co.uk](mailto:joseph.wright@morningstar2.co.uk).
