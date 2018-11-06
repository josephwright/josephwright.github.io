---
id: 856
title: Installing achemso and siunitx
date: 2010-12-27T21:36:16+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=856
permalink: /2010/12/27/installing-achemso-and-siunitx/
categories:
  - achemso
  - Packages
  - siunitx
tags:
  - installation
---
A question that comes up from time to time is how to install one or other of my packages, usually either [achemso](http://ctan.org/pkg/achemso) or [siunitx](http://ctan.org/pkg/siunitx). While both are essentially standard LaTeX packages (no weird files or binaries needed), there are still soem stumbling blocks that cause issues. So I thought a few notes by be useful here.

## Installing as part of an up to date TeX system

By far the easiest way to install my LaTeX packages is to get them as part an up to date TeX system. Both [MikTeX 2.9](http://www.miktex.org/) and [TeX Live 2010](http://www.tug.org/texlive) include all of my general packages. MiKTeX is of course Windows-only, but TeX Live can be installed on Windows, Mac OS X and Linux. After installation, doing an on-line update should grab all of the latest packages from [CTAN](http://www.ctan.org/). Both MiKTeX and TeX Live include graphical update programs, so this is not such a difficult process nowadays.

Mac users may well prefer [MacTeX](http://www.tug.org/mactex) over plain TeX Live, but MacTeX is built on top of TeX Live and so the same ideas apply. You can install either TeX Live or MacTeX and get the same basic functionality.

For Linux users, it's worth noting that popular Linux distributions tend to include old versions of TeX Live (or even teTeX), rather than TeX Live 2010. So if you want an up-to-date TeX system you'll be better off ignoring your Linux package manager and grabbing TeX Live directly.

One thing to do if you update your TeX system is to check any locally-installed files you might have (see the next section for more about local installation). These will be in `~/texmf` on Linux, `~/Library/texmf` on a Mac and (probably) `%USERPROFILE%\texmf` on Windows. One problem I see from time to time is that users of achemso have installed some of the BibTeX styles locally, then update the main package and all sorts of things go wrong. So do check carefully on any local files: they might be outdated by a new TeX system.

## Installing using the TDS zip files

The method above is fine if you are happy installing an entirely new TeX system, but if all you need is access to one of my packages then it is probably over-kill. For these users, I provide ready-to-install zip files on CTAN. For achemso, you need [achemso.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=achemso.tds.zip&amp;Search=Search), while for siunitx users you probably need

- [siunitx.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=siunitx.tds.zip&amp;Search=Search)
- [expl3.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=expl3.tds.zip&amp;Search=Search)
- [xpackages.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=xpackages.tds.zip&amp;Search=Search)

The idea with these files is that I have set them up with documentation, ready to use LaTeX styles and all of the support files. All that needs to happen with them is to unzip them inside your local TeX directory and tell TeX about them.

Where the files should go depends a little on your operating system. The local directory (folder) is usually `~/texmf` on Linux, `~/Library/texmf` on a Mac and (probably) `%USERPROFILE%\texmf` on Windows. Here, `~` and `%USERPROFILE%` represent your home directory (folder). So on my Windows 7 PC, I have a folder

```
C:\Users\joseph\texmf
```

while on my Mac there is one at

```bash
/Users/joseph/Library/texmf
```

Whichever system you use, copy the appropriate zip files there and unzip. The result should be a structure which looks like

```bash
texmf/tex/latex/achemso/achemso.sty
...
texmf/tex/latex/siunitx/siunitx.sty
```

and so on. Of course, the exact structure will depend on which packages you install! What is important for installing `siunitx` is to also install `expl3` and `xpackages`. If the versions do not match then trouble will not be far away.

To tell TeX about the new files, you need to run the program `texhash`. There is a graphical interface for this in both MiKTeX (_Update File Name Database_) and TeX Live. I find it easiest just to start a Command Prompt/Terminal and type

```bash
texhash
```

[For users with recent versions of TeX Live (2009 and 2010, I think), running `texhash` is actually not needed. However, it will not do any harm so you may as well run it.)

## Installing from the dtx file

The traditional method to install a package is to unpack it from the dtx source. I've got to say that I only recommend this for experienced LaTeX users. While both achemso and siunitx are designed to be easy to unpack, life is more complex for expl3 and xpackages. So I'd strongly recommed using the TDS zip files unless you know a bit more about LaTeX!
