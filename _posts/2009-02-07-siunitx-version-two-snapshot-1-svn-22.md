---
id: 162
title: 'siunitx version two: Snapshot 1 (SVN 22)'
date: 2009-02-07T20:02:32+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=162
permalink: /2009/02/07/siunitx-version-two-snapshot-1-svn-22/
categories:
  - Packages
  - siunitx
---
As promised a while ago, I've been working to get a snapshot of my work on [siunitx version 2](http://siunitx.berlios.de) ready. I've now got something that works “as far as it goes”, so I'm making a first snapshot available.  This is version control (SVN) repository revision 22, which you can see on [BerliOS](http://www.berlios.de). As this is a very earlier version of what I'm looking at, I'm just posting three files here:

- [The source (.dtx)](http://www.texdev.net/wp-content/uploads/2009/02/siunitx.dtx)
- [The user manual (.pdf)](http://www.texdev.net/wp-content/uploads/2009/02/siunitx.pdf)
- [The style file (.sty)](http://www.texdev.net/wp-content/uploads/2009/02/siunitx.sty)

Currently, only the `\num` macro works at all, and even then only for single numbers. However, there are several points to note for testers  and interested users:

1. The package understands complex numbers.
2. The options use [pgfkeys](https://ctan.org/pkg/pgf), although this may change.
3. Input and output of numbers are much more clearly separated, which makes extension much easier.
4. A number of subtle bugs in version one are fixed here. (No-one else seems to have noticed them, so for the moment I've not fixed them in the release version!)
5. Currently, only the new options are implemented, although before release the full set of version one options will be implemented.

Although the snapshot is not functional enough for general use, I'd appreciate any feedback people can give.  There are probably some bugs in the number code, which obviously I'd like to hear about.  The new option arrangement is something I'd like to get opinions on.  I feel it is much more logical (and easier to extend as new ideas arrive), but I'm obviously keen to see how others see it.
