---
title: QuickLaTeX&#58; A LaTeX plugin for WordPress
layout: post
permalink: /2011/02/10/quicklatex-a-latex-plugin-for-wordpress/
categories:
  - General
tags:
  - LaTeX
  - QuickLaTeX
  - WordPress
---
[latexpage]
Reading through the chat page for the [{TeX} Q&amp;A](https://tex.stackexchange.com/) site today, I stumbled upon a reference to [QuickLaTeX](http://www.holoborodko.com/pavel/quicklatex/). This is a plugin for [WordPress](http://www.wordpress.org/) to allow you to show LaTeX code in your page or blog. That's not unique, but what is interesting is that it runs the LaTeX on the QuickLaTeX server, meaning that you don't need LaTeX on your web host's system. For me, that was immediately interesting as I don't have a TeX installation on the host for this site. (It looks like QuickLaTeX is built using [TeX Live 2010](https://tug.org/texlive), so most packages should be available unless you are on the bleeding-edge.)

The system seems pretty easy to use. The plugin follows the standard WordPress model: download, install and activate. The [plugin page](http://www.holoborodko.com/pavel/quicklatex/#gstarted) gives some details on how to use it, but a few examples here will show off the power of the system. It's possible to put something simple into the blog, such as

```latex
!\[ y = mx + c \]
```

and get
\[ y = mx + c \]
or something much more complex, like

```latex
!\begin{tikzpicture}
[+preamble]
\usepackage{tikz}
\usepackage{pgfplots}
\pgfplotsset{compat=newest}
[/preamble]
\begin{axis}
\addplot3[surf,domain=0:360,samples=40] {cos(x)*cos(y)};
\end{axis}
\end{tikzpicture}
```

and get
\begin{tikzpicture}
[+preamble]
\usepackage{tikz}
\usepackage{pgfplots}
\pgfplotsset{compat=newest}
[/preamble]
\begin{axis}
\addplot3[surf,domain=0:360,samples=40] {cos(x)*cos(y)};
\end{axis}
\end{tikzpicture}
All that is needed, beyond the plugin, is to put `![latexpage]` at the start of the page. You can then escape any 'raw' LaTeX by prefixing the beginning with `!`, for example

```latex
!!\[ y = mx + c \]
```

is what I used for the first of my demos.

I don't often find the need to post actual LaTeX examples in my blog, but the facility is certainly one I'm happy to have access to. The license for QuickLaTeX asks for a public link to their site, which seems like a small pay-off for a very handy service.
