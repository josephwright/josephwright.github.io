---
title: 'TeX on Windows: MiKTeX or TeX Live'
layout: post
permalink: /2011/11/19/tex-on-windows-miktex-or-tex-live/
categories:
  - General
tags:
  - MiKTeX
  - TeX Live
  - Windows
---
Around two years ago, I wrote a [short post comparing MiKTeX and TeX Live for Windows-based TeX users](/2009/11/07/windows-tex-users-miktex-or-tex-live/). Looking at my log files, this topic is perhaps the most common search term that brings people here. As such, I think it's time to revisit the question and bring what I said before up to date.

On Windows, there are two actively-developed TeX systems with similar coverage: [MiKTeX](https://www.miktex.org/) and [TeX Live](https://tug.org/texlive). Before I look at the comparison, a reminder that they are not the only choices. [W32TeX](http://w32tex.org/) is popular in the far east, and as well as being a TeX system in its own right is the source of the Windows binaries for TeX Live. There are also the commercial [BaKoMa](http://www.bakoma-tex.com/) and [VTeX](http://www.micropress-inc.com/) systems (although whether anyone can get hold of the supplier of the latter is another question). However, for most users it comes down to a choice between the ‘big two’.

The good news is that there is a lot of similarity between the two systems, so for most users both systems are equally usable. However, there are differences and depending on what you need these might be important.

- The standard settings install _everything_ for TeX Live, but only a minimal set of packages for MiKTeX. MiKTeX will then install extra packages ‘on the fly’, while TeX Live does not (there is a [package to do that in TeX Live](https://ctan.org/pkg/texliveonfly), but it's aimed at Linux). Install-on-the-fly is useful if space is limited, but is more problematic on server set ups. So this is very much a feature who's usefulness depends on your circumstances. Of course, there is nothing to stop you using MiKTeX and installing everything.
- The [xindy](http://www.xindy.org/) program is only available in TeX Live. For those of you not familiar with it, xindy is an index-processor, and is much more capable of dealing with multi-lingual situations than MakeIndex. If you need xindy, TeX Live really is the way to go.
- MiKTeX is very much a Windows tool set, while TeX Live comes from a Unix background. This shows up from time to time in the way TeX Live is administered, and the fact that the TeX Live GUI is written based on Perl rather than as a ‘native’ Windows application.
- As TeX Live is the basis of [MacTeX](https://tug.org/mactex), and is _the_ TeX system for Unix, if you work cross-platform and want an identical system on all of your machines, then TeX Live is the way to go.

