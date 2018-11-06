---
id: 382
title: Cross-platform working
date: 2009-08-18T20:49:12+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=382
permalink: /2009/08/18/cross-platform-working/
categories:
  - General
tags:
  - 7-Zip
  - CTAN
  - Info-Zip
  - TDS
  - Unix
  - Windows
---
As many people will know, the [CTAN](https://www.ctan.org) team have come up with the idea of having TDS-ready zip files for packages. The idea is that you can just download the zip into your local TeX directory, unzip it and run texhash, with no TeX-based unpacking or document compilation.

That's all fine when it works, but I've recently had a bit of trouble making zips at my end. My favoured tool for doing that has tended to be [7-Zip](http://www.7-zip.org). However, it was pointed out to me last week that the resulting zip files are not quite right. On Unix systems, the command `unzip -xa` will convert line endings to the system convention (LF only), even if they come from Windows (LF-CR endings). However, this requires that the zip identifies text files, and 7-Zip marks everything as binary!

I did a bit of hunting around, and found [Info-ZIP](http://www.info-zip.org), where after a bit of hunting about you can find `zip` and `unzip` binaries for Windows. These give me Unix-like capabilities on Windows, so I can make the appropriate files, alter line endings on zipping/unzipping and check the results.

That led me to take another look at the batch file I use  each time I release something to CTAN: doing it by hand is an unreliable business!  I've reworked it quite a bit, to generalise everything and also add a few tweaks. For anyone interested, the file is [available here](http://www.texdev.net/wp-content/uploads/2009/08/make.bat). It's called make, so that you get Unix-like abilities on Windows. The file has to be customised for each package I write, but most of this version is generalised, and can be altered using a few settings.

```bat
set AUXFILES=aux cmds dvi glo gls hd idx ilg ind ist log los out tmp toc
set CLEAN=bib bst cls eps gz ins cfg pdf sty tex txt zip
set DOCEXTRA=\AtBeginDocument{\OnlyDescription}
set INDEXFILE=gglo
set PACKAGE=achemso
set PDF=%PACKAGE%
set TDSROOT=latex\%PACKAGE%
set TEX=achemso-demo
set TXT=README
set UNPACK=%PACKAGE%.dtx
```

Anyone at all familiar with batch files will see that this is a block of environmental variables: in this case, these are the settings for my [achemso](https://ctan.org/pkg/achemso) package. Most are pretty obvious settings, but in case anyone wants to use the file for their own purposes:

- `AUXFILES` File types to delete after every run: throw away files.
- `CLEAN` File types deleted only if make clean is run: useful stuff.
- `DOCEXTRA` Inserted when creating documentation, can be anything. I don't typeset the code for my packages in the release documents, hence the `\OnlyDescription` setting.
- `INDEXFILE` This is always `gglo` for documents using the `ltxdoc` class, but is `l3doc` if using the LaTeX3 class `l3doc`.
- `PACKAGE` Pretty obvious, the bundle name!
- `PDF` The names of PDF files to add to the documentation part of a TDS zip. By having this as a setting, special effects (demo documents, for example) are possible.
- `TDSROOT.` Almost always as given for a LaTeX package.
- `TEX` A list of .tex files to copy into the TDS archive: to avoid any testing files, not all .tex files are copied.
- `TXT` The names of text files to copy to the documentation directory
- `UNPACK` The file(s) to run to unpack the package. I use .dtx files that are self-extracting, but the traditional method is to have a separate .ins file.

If the batch file proves useful to enough people, I might write some proper documentation and do a bit more generalisation.

With all of that in place, I can hopefully keep Unix-based LaTeX users happy without too much work!
