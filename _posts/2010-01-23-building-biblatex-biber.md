---
id: 611
title: Building biblatex-biber
date: 2010-01-23T20:24:56+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=611
permalink: /2010/01/23/building-biblatex-biber/
categories:
  - biblatex
  - Packages
tags:
  - biber
  - Perl
---
The [biblatex-biber](http://biblatex-biber.sourceforge.net/) project provides probably the best way for [biblatex](http://ctan.org/pkg/biblatex) users to switch to pure UTF-8 bibliography information. However, getting it to build can cause problems: biblatex-biber is a [Perl](http://www.perl.org/) programme, and needs various downloads from [CPAN](http://www.cpan.org/). I thought it would therefore be useful to put some simple recipes here, explaining what I've done to get a working biblatex-biber on Windows, Ubuntu and Mac OS X. I'm assuming that the latest biblatex-biber release has been downloaded and unzipped somewhere, and that the Command Prompt/Terminal/Shell is open in that directory (folder).

## Mac OS X 10.6 (Snow Leopard)

Mac OS X comes with Perl installed, so life is relatively easy. At the Terminal, you need to run the `cpan` script as root:

```bash
sudo cpan
```

The cpan script has its own prompt, but this is very similar to the Terminal one. First, I updated `cpan` itself and installed a helper module with

```bash
install CPAN
reload cpan
install YAML
```

That done, the various requirements for biblatex-biber can be installed, using the single call

```bash
install Data::Dump List::AllUtils Readonly Text::BibTeX Readonly::XS
```

For the more cautious person (such as me), each `install` instruction can be given on a separate line: this keeps things a bit more controlled. I accepted the standard settings, except when asked about installing items that were only needed for testing, where I said no.

Once `cpan` has done all of the installing, you can leave it by typing

```bash
exit
```

So now back at the Terminal prompt, a few simple instructions

```bash
perl Build.PL
./Build
sudo ./Build install
```

That put biblatex-biber onto the path for all users: everything then worked correctly.

## Ubuntu 9.10

Once again, Perl is installed as standard in Linux distributions: I'm using [Ubuntu](http://www.ubuntu.com/) as a representative system. Before starting `cpan`, there is an additional step, which is to install an extra Ubuntu package. So at the Terminal, you need to do

```bash
sudo apt-get install libxml2-dev
```

This is needed as otherwise you get some very odd errors in a bit. Now, essentially the same recipe works as for the Mac. First run `cpan` running and update and install `YAML`. Then there is a long list of items to install

```bash
install Data::Dump List::AllUtils Readonly Text::BibTeX Readonly::XS XML::Writer XML::LibXML File::Slurp
```

which can again be done one at a time, for the more cautious.

After exiting `cpan`, the same three lines at the Terminal should work as in the Mac section.

```bash
perl Build.PL
./Build
sudo ./Build install
```

## Windows (XP, Vista and 7)

To date, my attempts to build biblatex-biber on Windows (using [Strawberry Perl](http://strawberryperl.com/)) have failed as I can't get the Perl module `Text::BibTeX` to install. This is supposed to be optional, but without it biblatex-biber does not seem to work, although I do get it to build. Luckily, there is a self-contained binary for Windows available from the project site. This includes its own Perl system, so there is no need to get Perl set up before trying it. Everything seems to work for me with this version. Any ideas on what is necessary would be helpful!
