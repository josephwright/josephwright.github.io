---
id: 395
title: TeX Live on Windows
date: 2009-08-23T18:49:25+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=395
permalink: /2009/08/23/tex-live-on-windows/
categories:
  - General
tags:
  - MiKTeX
  - TeX Live
  - Windows
---
As I <a href="http://www.texdev.net/2009/08/02/testing-miktex-2-8-and-tex-live-2009/">posted earlier</a>, the upcoming releases of both <a title="MiKTeX Project Page" href="http://www.miktex.org/">MiKTeX</a> and <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> have very similar sets of features on Windows. I've just stumbled upon something that points up the slight differences that exist, even though this one is a bit complicated.

To detect what system is being used, for things like shell escape tricks, there is a LaTeX package called <a title="Conditionals to test which platform is being used" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=ifplatform">ifplatform</a>. However, this only works on Windows if MiKTeX is being used. The reason is that while TeX Live aims to be as similar as possible across platforms, MiKTeX can adopt a different approach and stick to Windows conventions. Most of the time, this is transparent but it shows up if you use the <code>-shell-escape</code> option for either system and try to do some testing. Inside ifplatform, you'll find the lines:
<pre>\edef\ip@sig{write18-test-\the\year\the\month\the\day\the\time}
\edef\ip@win{'\ip@sig'}
\immediate\write18{echo \ip@win &gt;"\ip@file"}</pre>
The idea is that the text written to the temporary file will be different on Windows to on a Unix-like system. MiKTeX will retain the single quotes around the test data:
<pre>'write18-test-20098231074'</pre>
whereas Unix-like systems will not:
<pre>write18-test-20098231074</pre>
But try using ifplatform with TeX Live on Windows and the test fails. First, no test file gets written at all: a bit of hacking leads to the change of the write line to
<pre>\immediate\write18{echo \ip@win &gt; \ip@file}</pre>
and then at least the first step works. However, the test file now looks like a Unix one (with no quote marks), and ifplatform gets things wrong. So for the moment the only thing to do is create a stub package file and use it, something like:
<pre>\ProvidesPackage{ifplatform}[2007/11/18 v0.2  Testing for the operating system]
\newif\ifshellescape\shellescapetrue
\newif\ifwindows\windowstrue
\newif\ifmacosx
\newif\iflinux</pre>
I've reported the problem to Will Robertson, and hopefully a solution which really tests the OS rather than the TeX system can be found. However, it is a reminder that even with very general feature sets, the two major TeX distributions still act differently in some respects when used on Windows.
