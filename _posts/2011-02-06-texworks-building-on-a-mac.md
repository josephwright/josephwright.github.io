---
id: 913
title: 'TeXworks: building on a Mac'
date: 2011-02-06T11:38:29+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=913
permalink: /2011/02/06/texworks-building-on-a-mac/
categories:
  - TeXworks
---
Development of [TeXworks](http://www.texworks.org/) has picked up over the last couple of months, with a drive to get to version 0.4. Several builds for Windows have been posted on the [TeXworks downloads page](http://code.google.com/p/texworks/downloads/list), so testing there has been pretty easy. For Linux users, the [instructions for building from source](http://code.google.com/p/texworks/wiki/Building) are not too bad, so anyone wanting to test on Linux has also been okay. However, Mac users face more a more difficult time. The last official binaries were posted in February 2010, and most Mac users don't build software from the sources.

There was a [post to the TeXworks mailing list](https://tug.org/pipermail/texworks/2011q1/003738.html) yesterday asking for volunteers to get Mac binaries sorted out. This will not be a trivial process: Mac OS X is used on PowerPC and Intel chips, and the later covers both 32- and 64-bit cases. However, the aim has to be first to solve the more basic problem of getting the software to build at all! [Bruno Voisin](https://tug.org/pipermail/texworks/2011q1/003764.html) has managed that, but this is a test case and not really suitable for distribution.

As I've got a Mac, I'm having a go at solving some of the problems, but my experience with serious programming is pretty much non-existent, so whether I'll be much help I'm not sure. So any keen TeX-using Mac programmers reading might want to take a look at the discussion and make suggestions (or of course provide some binaries and build instructions!).
