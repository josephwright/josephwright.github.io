---
title: Building Biber on Ubuntu 10.04 (Lucid Lynx)
layout: post
permalink: /2010/05/06/building-biber-on-ubuntu-10-04-lucid-lynx/
categories:
  - biblatex
  - Packages
tags:
  - Biber
  - Ubuntu
---
As I've [just installed](/2010/05/06/tex-live-2009-on-ubuntu-10-04-lucid-lynx/) Ubuntu 10.04 ('Lucid Lynx') on my test system, I thought I should check that I can get [Biber](http://biblatex-biber.sourceforge.net/) working. As in my [earlier posts](/index.php?s=biber), this is not too hard, but it's nice to have some instructions. As usual, first you need to download Biber from the homepage and unpack the files. Using the Terminal, move the directory where the source is and do

```bash
sudo cpan Config::AutoConf
perl Build.PL
sudo ./Build installdeps
./Build
./Build test
sudo ./Build install
```

The `cpan` line adds one module to Perl which for some reason Biber's `installdeps` routine doesn't find automatically: if you miss this out then the build will fail. There are a lot of Perl questions while the additional modules are installed: I just say yes to all to them. The build itself is pretty quite, and it's almost at the point of being trivial (the above instructions now seem to work on all the platforms I use).
