---
id: 659
title: Building biblatex-biber on Windows
date: 2010-04-01T12:14:00+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=659
permalink: /2010/04/01/building-biblatex-biber-on-windows/
categories:
  - biblatex
  - Packages
tags:
  - biber
  - Perl
---
I've just reinstalled my [Strawberry Perl](http://strawberryperl.com/) system on Windows, and so had the opportunity to try a clean build of [biblatex-biber](http://biblatex-biber.sourceforge.net/). I've [posted before](/2010/02/27/building-biblatex-biber-again/) about building this on various platforms, and it now is almost asstraight-forward on Windows as on Linux.

As before, I'll assume you've grabbed the source code, unzipped it and have a Command Prompt running as the Administrator, in the directory where biblatex-biber is unzipped. First, you need to install one support Perl module using

```bash
cpan Config::AutoConf
```

You can then do

```bash
perl Build.PL
build installdeps
build
build test
build install
```

That's it! I'm not quite sure why you have to install Config::AutoConf ‘by hand’, but if you don't then Text::BibTeX still fails to work. However, that is almost as easy as on Linux or MacOS 10.6, so everyone should be able to use biblatex-biber now.
