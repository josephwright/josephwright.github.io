---
id: 1046
title: Spaces in file names
date: 2011-07-16T07:45:40+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1046
permalink: /2011/07/16/spaces-in-file-names/
categories:
  - General
tags:
  - MiKTeX
  - TeX Live
---
Spaces in file names are a constant issue for LaTeX users. As many people will know, TeX is not really very happy with spaces, as they are used to delimit the end of input in a lot of low-level macros. This shows up particularly in two areas: graphics and shell escape. For graphics, the excellent [`grffile`](https://ctan.org/pkg/grffile) package will deal with many of the issues. When using shell escape, the issue is usually that `\jobname` may be slightly odd. For TeX Live users, that is not so much of a problem as the name is automatically quoted to protect the space. However, MiKTeX does things a bit differently, and uses a star in place of a space. So you end up with

```latex
\edef\example{\jobname}
\show\example
&gt; \example=macro:
-&gt;test*file.
l.2 \show\example
```

which is not exactly helpful. However, it is possible to deal with this, as [recently mentioned on TeX.SX](https://tex.stackexchange.com/q/14949/73). As `*` cannot normally appear in file names, and `\jobname` makes all characters have category code 12, a simple approach is to do a quick replacement

```latex
\edef\Jobname{\jobname}
\catcode`\*=\active
\def*{ }
\edef\Jobname{"\scantokens\expandafter{\Jobname\noexpand}"}
\catcode`\*=12 %
\show\Jobname
```

If you want to deal with both TeX Live and MiKTeX, you'd of course need first to test which system is in use (for example using `\pdftexbanner`).
