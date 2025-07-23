---
title: TeX Live 2009 on Ubuntu 10.04 (Lucid Lynx)
layout: post
permalink: /2010/05/06/tex-live-2009-on-ubuntu-10-04-lucid-lynx/
categories:
  - General
tags:
  - TeX Live
  - Ubuntu
---
TeX users on Linux tend to use the packaged TeX installation provided by there distro, rather than using the standard [TeX Live](https://tug.org/texlive/) installer and managing things themselves. [Ubuntu](http://www.ubuntu.com/) is one of the more popular Linux distros, and there has been an issue for a while that they had stuck with TeX Live 2007, despite TeX Live 2008 and then TeX Live 2009 being released.

The latest Ubuntu release, 10.04 'Lucid Lynx', finally moves to TeX Live 2009. This finally makes it easy to get TeX Live in a reasonable up to date version:

```bash
sudo apt-get install texlive
```

This grabs a subset of the complete TeX Live 2009, but seems to include quite a good selection (a bit like the [MiKTeX](https://www.miktex.org/) basic installation on Windows, but I think a bit bigger). TeXworks is also on the list (at least the stable version), so if you don't want to compile it from the source you can do

```bash
sudo apt-get install texworks
```

and be ready to go. Of course, you might still need to grab a few more bits of TeX Live (for example, [XeTeX](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=xetex) is not included in the standard selection). However, it's definitely an improvement of the earlier situation.
