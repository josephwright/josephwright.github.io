---
title: TeX Live on Windows
layout: post
permalink: /2009/08/23/tex-live-on-windows/
categories:
  - General
tags:
  - MiKTeX
  - TeX Live
  - Windows
---
As I [posted earlier](/2009/08/02/testing-miktex-2-8-and-tex-live-2009/), the upcoming releases of both [MiKTeX](https://www.miktex.org/) and [TeX Live](https://tug.org/texlive/) have very similar sets of features on Windows. I've just stumbled upon something that points up the slight differences that exist, even though this one is a bit complicated.

To detect what system is being used, for things like shell escape tricks, there is a LaTeX package called [`ifplatform`](https://ctan.org/pkg/ifplatform). However, this only works on Windows if MiKTeX is being used. The reason is that while TeX Live aims to be as similar as possible across platforms, MiKTeX can adopt a different approach and stick to Windows conventions. Most of the time, this is transparent but it shows up if you use the `-shell-escape` option for either system and try to do some testing. Inside `ifplatform`, you'll find the lines:

```latex
\edef\ip@sig{write18-test-\the\year\the\month\the\day\the\time}
\edef\ip@win{'\ip@sig'}
\immediate\write18{echo \ip@win >"\ip@file"}
```

The idea is that the text written to the temporary file will be different on Windows to on a Unix-like system. MiKTeX will retain the single quotes around the test data:

```bash
'write18-test-20098231074'
```

whereas Unix-like systems will not:

```bash
write18-test-20098231074
```

But try using `ifplatform` with TeX Live on Windows and the test fails. First, no test file gets written at all: a bit of hacking leads to the change of the write line to

```latex
\immediate\write18{echo \ip@win > \ip@file}
```

and then at least the first step works. However, the test file now looks like a Unix one (with no quote marks), and `ifplatform` gets things wrong. So for the moment the only thing to do is create a stub package file and use it, something like:

```latex
\ProvidesPackage{ifplatform}[2007/11/18 v0.2  Testing for the operating system]
\newif\ifshellescape\shellescapetrue
\newif\ifwindows\windowstrue
\newif\ifmacosx
\newif\iflinux
```

I've reported the problem to Will Robertson, and hopefully a solution which really tests the OS rather than the TeX system can be found. However, it is a reminder that even with very general feature sets, the two major TeX distributions still act differently in some respects when used on Windows.
