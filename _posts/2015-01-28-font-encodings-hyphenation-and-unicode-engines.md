---
id: 1785
title: Font encodings, hyphenation and Unicode engines
date: 2015-01-28T21:31:51+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1785
permalink: /2015/01/28/font-encodings-hyphenation-and-unicode-engines/
categories:
  - General
tags:
  - encodings
  - fonts
  - Unicode
---
The LaTeX team have over the past couple months been taking a good look at the Unicode TeX engines, XeTeX and LuaTeX, and making [efforts to make the LaTeX2e kernel more 'Unicode aware'](/2015/01/17/latex2e-and-unicode-engines-the-detail/). We've now started looking at an important question: moving documents from pdfTeX to XeTeX or LuaTeX. There are some important differences in how the engines work, and I've discussed some of them in a [TeX StackExchange post](http://tex.stackexchange.com/a/222300/73), but here I'm going to look at one (broad) area in particular: font encodings and hyphenation. To understand the issues, we'll first need a bit of background: first for 'traditional' TeX then for Unicode engines.

Knuth's TeX (TeX90), e-TeX and pdfTeX are all 8-bit programs. That means that each font loaded with these engines has 256 slots available for different glyphs. TeX works with numerical character codes, not with what we humans think of as characters, and so what's happening when we give the input

```latex
\documentclass{article}
\begin{document}
Hello world
\end{document}
```

to produce the output is that TeX is using the glyph in position 72 of the current font ('H'), then position 101 ('e'), and so on. For that to work and to allow different languages to be supported, we use the concept of font encodings. Depending on the encoding the relationship between character number and glyph appearance varies. So for example with

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
\char200
\end{document}
```

we get 'È' but with

```latex
\documentclass{article}
\usepackage[T2A]{fontenc}
\begin{document}
\char200
\end{document}
```

we get 'И' (T2A is a Cyrillic encoding).

This has a knock-on effect on dealing with hyphenation: a word which uses 'È' will probably have very different allowed hyphenation positions from one using 'И'. 'Traditional' TeX engines store hyphenation data ('patterns') in the format file, and to set that up we therefore need to know which encoding will be used for a particular language. For example, English text uses the T1 encoding while Russian uses T2A. So when the LaTeX format gets built for pdfTeX there is some code which selects the correct encoding and does various bits of set up for each language before reading the patterns.

Unicode engines are different here for a few reasons. Unicode doesn't need different font encodings to represent all of the glyph slots we need. Instead, there is a much clearer one-to-one relationship between a slot and what it represents. For the [Latin-1](http://en.wikipedia.org/wiki/ISO/IEC_8859-1) range this is (almost) the same as the T1 encoding. However, once we step outside of this all bets are off, and of course beyond the 8-bit range there's no equivalent at all in classical TeX. That might sound fine (just pick the right encoding), but there's the hyphenation issue to watch. Some years ago now the hyphenation patterns used by TeX were translated to Unicode form, and these are read natively by XeTeX (more on LuaTeX below). That means that at present XeTeX will only hyphenate text correctly if it's either using a Unicode font set up or if it's in a language that is covered by the Latin-1/T1 range: for example English, French or Spanish but not German (as `ß` is different in T1 from the Latin-1 position).

LuaTeX is something of a special case as it doesn't save patterns into the format and as the use of 'callbacks' allows behaviour to be modified 'on the fly'. However, at least without some precautions the same ideas apply here: things are not really quite 'right' if you try to use a traditional encoding. (Using LuaLaTeX today you get the same result as with XeTeX.)

There are potential ways to fix the above, but at the moment these are not fully worked out. It's not also clear how practical they might be: for XeTeX, it seems the only 'correct' solution is to save all of the hyphenation patterns twice, once for Unicode work and once for using 'traditional' encodings.

What does this mean for users? Bottom line: don't use `fontenc` with XeTeX or LuaTeX unless your text is covered completely by Latin-1/T1. At the moment, if you try something as simple as

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
% A quick test to use inputenc only with pdfTeX
\ifdefined\Umathchar\else
  \usepackage[utf8]{inputenc}
\fi
\begin{document}
straße
\end{document}
```

then you'll get a surprise: the output is wrong with XeTeX and LuaTeX. So working _today_ you should (probably) be removing `fontenc` (and almost certainly loading `fontspec`) if you are using XeTeX or LuaTeX. The team are working on making this more transparent, but it's not so easy!
