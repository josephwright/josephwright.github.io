---
id: 603
title: PDF Version and file size
date: 2010-01-11T19:28:24+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=603
permalink: /2010/01/11/pdf-version-and-file-size/
categories:
  - General
tags:
  - Acrobat
  - PDF
  - pdfTeX
---
The PDF format has evolved over the years as [Adobe](http://www.adobe.com/) have released new versions of their [Acrobat](http://www.adobe.com/products/acrobat/) and [Reader](http://get.adobe.com/uk/reader/) software. New ideas have been added to the file format, and as a result there are different versions of the PDF format. If you take a look at a PDF in Adobe Reader, you can see which version the file is using in the Document Properties information. Of course, files using the newer versions of the PDF format need a suitable viewer, be that Reader or something else.

This is relevant to TeX users as PDF tends to be the target format, either directly or via DVI files, for many users. Tools such as [pdfTeX](http://www.pdftex.org/) are not tied to one version of the PDF specification. For example, when creating a PDF directly with pdfTeX the `\pdfminorversion` primitive can be used to set the PDF version to 1.3, 1.4 or 1.5.

Why would you want to do this? Well, obviously the newer versions bring new features. A particularly significant one is the compression of _non-stream objects_. The detail of these objects is not really important, but they relate to items such as links within documents. Version 1.5 of the PDF specification allows these to be compressed, which can make quite a difference to the resulting file size. For example, I did a trial run with the [`siunitx`](https://ctan.org/pkg/siunitx) manual, and by adding the lines

```latex
\pdfminorversion=5
\pdfobjcompresslevel=2
```

resulted in reducing the file size from around 700 KiB to around 550 KiB, a saving of roughly 20 %.

There is some discussion ongoing at the moment on the [TeX Live mailing list](http://tug.org/mailman/listinfo/tex-live) about possibly changing the default PDF version produced by tools such as pdfLaTeX, XeLaTeX, _etc_. The current standard setting is version 1.4, which makes larger files but does have the advantage of being readable by a wider range of viewers. On the other hand, PDF version 1.5 was first released in 2003, and there is pretty good support for it in most of the well-known readers. As long as switching to version 1.5 also enables the compression, this looks like a good idea: just moving to version 1.5 without using the features available seems a bit odd to me.

There are times where you need to use PDF version 1.4 (for example for archive-type PDFs), but for those you also need to check other features of the PDF. So I feel that the change looks like a good idea, provided there is a good way to set the version to something else.
