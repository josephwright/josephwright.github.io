---
id: 591
title: siunitx performance
date: 2009-12-28T22:43:20+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=591
permalink: /2009/12/28/siunitx-performance/
categories:
  - Packages
  - siunitx
tags:
  - speed
---
I had an e-mail today about using <a title="A comprehensive (SI) units package" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=siunitx">siunitx</a> when there are a lot of calls to the package. As you might expect, things can get a bit slow, and the person who contacted me felt that things get rather too slow. There are differences between the current release version of siunitx and the development code (version 2), and I've also added a few features to help speed things up where appropriate using version 2. So I thought I'd put a bit of information on the comparison in the public domain.

First, a baseline is not to use siunitx at all, and to simply test everything by hand. For that, I tried the simple test file:
<pre>\documentclass{article}
\usepackage{siunitx,xparse}
\ExplSyntaxOn
\DeclareDocumentCommand \repeated { m m }{
  \prg_replicate:nn {#1} {#2}
}
\ExplSyntaxOff
\begin{document}

\repeated{10000}{$1.23\,\text{m}$ }

\end{document}
</pre>
This repeats the same text 10 000 times: boring but handy for testing. Using the command-line <code>time</code> program, I get an overall time of 1.714 s for this.

A very slight change of the file lets me test with siunitx version 1:
<pre>\documentclass{article}
\usepackage{siunitx,xparse}
\ExplSyntaxOn
\DeclareDocumentCommand \repeated { m m }{
  \prg_replicate:nn {#1} {#2}
}
\ExplSyntaxOff
\begin{document}

\repeated{10000}{\SI{1.23}{\metre} }

\end{document}
</pre>
With the latest release version of siunitx (v1.3g), I get a time of 80.878 s for this on the same system.

In siunitx version 2, I've recoded all of the loops and parsing code, and so things are faster using the standard settings: 58.944 s. With the very latest code (SVN 243), I've included two options to make things move faster: <code>parse-numbers</code> and <code>parse-units</code>. Of course, these do mean that you get less of the power of siunitx. But for many people they might be useful. Turning both parsing systems off, the time needed for the test file drops to 14.975 s (just turning off the number parser gives a time of 18.803 s).

I may take another look at trying to improve the performance of the number parser. The problem is at least in part that making the code faster will either mean making some of it less powerful or, more likely, a lot harder to read and maintain. I hope that for most people, most of the time, the performance is acceptable. Of course, at some point I'll try to do some Lua-based code for the parsers, at least. But that won't help for most users now.

Ultimately, there is a limit to how fast things can work. Whether the performance hit of using siunitx is worthwhile is something is down to users. I think it's worth it, as the better logic in the mark-up more than makes up for the extra time required. But then I would say that!