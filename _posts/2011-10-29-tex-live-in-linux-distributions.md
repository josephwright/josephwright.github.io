---
id: 1123
title: TeX Live in Linux distributions
date: 2011-10-29T14:36:21+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1123
permalink: /2011/10/29/tex-live-in-linux-distributions/
categories:
  - General
tags:
  - Linux
  - TeX Live
---
A subject which comes up quite a bit is the age of TeX Live systems shipped with common Linux distributions. While the current ‘vanilla’ release is [TeX Live 2011](http://tug.org/texlive), many Linux distributions use TeX Live 2009, or even TeX Live 2007. This leaves many people wondering why. Now, I'm no expert in this area, but reading the various mailing lists gives me some ideas about the ‘time lag’. Some of this is technical, and some is more conceptual.

The first thing to say is that for many Linux users with a personal system, where they can install vanilla TeX Live each year directly from [TUG](http://tug.org/), it's probably easiest to simply not worry about this entire area and simply install TeX Live themselves. However, a lot of Linux systems are either multi-user or server set ups, and it's there that a lot of the following is more important.

The technical reason for the delay seems to be the way binaries are ‘linked’ to standard support libraries. To understand this, you first need to know that most programs use third-party code for standard tasks. So for example pdfTeX uses libraries for both `.png` and PDF support. In the vanilla TeX Live system (on Linux and other systems) these links are ‘static’, and the appropriate support material is supplied as part of the entire bundle. However, Linux distributions link ‘dynamically’. The advantage of the latter approach is that you only have one version of each library installed, and it is easy to update (for example for security fixes).  So re-bundling TeX Live for Linux means building the binaries using dynamic linking. That of course means doing some work, and this is not trivial.

Size is the second stumbling block. TeX Live is big, as it includes a lot of (La)TeX packages and more importantly all of the documentation, mainly in PDF format. On a modern system, the hit in terms of hard disk space is not usually an issue, but at the same time there's pressure in the Linux world to keep systems small and only install what is needed. So there is work to do in dividing TeX Live up into the constituent parts, a task that seems pretty difficult to me.

Finally, there is a conceptual point. TeX Live is not a single ‘product’, but is instead a bundle of different items from hundreds of different contributors. So while there is an overall TeX Live version, this does not reflect the status of each constituent part. The Linux packaging approach works best when each package has a small development team and a single version. It's not really so well adapted to the much more diffuse status of items in TeX Live. So you often see discussions about stability, that probably make sense for a single software package but fits much less well for TeX systems.

As I said above, for single-user systems where the user can update TeX Live each year it's probably easiest to simply bypass all of this. It's also worth noting that having TeX Live available is a lot better than the alternative.
