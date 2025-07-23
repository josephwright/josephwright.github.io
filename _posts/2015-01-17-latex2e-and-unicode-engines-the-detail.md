---
title: "LaTeX2e and Unicode engines: the detail"
layout: post
permalink: /2015/01/17/latex2e-and-unicode-engines-the-detail/
categories:
  - General
---
As I mentioned in my [last post](/2014/12/28/fixing-latex2e/), the LaTeX team are working on various small but important improvements to the LaTeX2e kernel. One area we are looking at is adjusting how the 'vanilla' format works with Unicode engines. I've been asked for a bit more detail on this area, so I'll try to fill in what's going on with the 'newer' engines.

To date, the 'vanilla' LaTeX format (`latex.ltx` and associated files) has been pretty much engine-neutral with no attempt to differentiate anything other than to deal with differences between TeX2 (7-bit, released 1982) and TeX3 (8-bit, released 1990). However, the LaTeX formats that almost all users actually load are not just made by running

```bash
<engine> -ini latex.ltx
```

(or similar). The 'format builders' [principally the [TeX Live](https://tug.org/texlive) team and Christian Schenk ([MiKTeX](http://miktex.org)] use a series of `.ini` files for building formats. For example, `pdflatex.ini`currently says

```latex
% Thomas Esser, 1998. public domain.
\input pdftexconfig.tex
\scrollmode
\input latex.ltx
\endinput
```

(The `.ini` files are in the main common to both TeX Live and MiKTeX. For building a pdfLaTeX that makes sense: `pdftexconfig.tex` just sets up related to direct PDF output as opposed to working in DVI mode. Things get more complicated, though, when we look at  the Unicode engines: some of the stuff is really 'general' and should be present in all LaTeX-based formats with these engines.

Both XeTeX and LuaTeX work with the entire Unicode range, so they need information on things like case mapping (`\lccode`/`\uccode`) and Unicode math handling (`\Umathcode`). The LaTeX format includes a `\dump` at the end, so without hacking about no code can be added _after_ it's loaded. More importantly, as XeTeX builds hyphenation into the format in the same way as 'classical' TeX the `\lccode` data needs to be right before the format loads the patterns. However, that can't be done just by reading data before `latex.ltx`: it sets up the 8-bit range for the T1 encoding scheme. That's an issue nowadays as the hyphenation patterns are nowadays stored in Unicode form: the stuff that happens 'behind the scenes' therefore (quite reasonably) assume that the Unicode engines can read these files with no 'trickery'. To accommodate this, at the moment you'll find that `xelatex.ini` includes

```latex
\input unicode-letters
% disable the \dump in latex.ltx
\expandafter\let\csname saved-dump-cs\endcsname\dump
\let\dump=\relax
\scrollmode
\input latex.ltx
```

and later

```latex
% Because latex.ltx sets up character code tables for T1 encoding by default,
% we need to reset values from unicode-letters that may have been overridden
\begingroup
\catcode`\@=11 \count@=128 % reset chars "80-"FF to category "other", no case mapp
ing
\loop \ifnum\count@<256
  \global\uccode\count@=0 \global\lccode\count@=0
  \global\catcode\count@=12 \global\sfcode\count@=1000
  \advance\count@ by 1 \repeat
\def\C #1 #2 #3 {\global\uccode"#1="#2 \global\lccode"#1="#3 } % case mappings (non-letter)
\def\L #1 #2 #3 {\global\catcode"#1=11 % category: letter
  \C #1 #2 #3 % with case mappings
  \ifnum"#1="#3 \else \global\sfcode"#1=999 \fi % uppercase letters have sfcode=999
  \global\XeTeXmathcode"#1="7"01"#1 % BMP letters default to class 7 (var), fam 1
  }
\def\l #1 {\L #1 #1 #1 } % letter without case mappings
[data lines]
\endgroup
\expandafter\let\expandafter\dump\csname saved-dump-cs\endcsname
\dump
```

There are some slight differences for `lualatex.ini`, but the general idea is the same. The need to 'hack around' the kernel is not great, and the team are much keener on the idea that it's a documented feature that the Unicode engines are set up for a Unicode encoding ('UC') rather than for T1. (I'll probably return to Unicode encodings in another context in a later post.)

As well as this important area, there are some things that are 'tacked on' to the formats by the `.ini` files but which apply only to one of either XeTeX or LuaTeX. For XeTeX, there is a need to manage the `\XeTeXinterchartoks` system, for which `xelatex.ini` currently does

<!-- {% raw %} -->
```latex
%
% Allocator for \XeTeXintercharclass values, from Enrico Gregorio
%
\catcode`\@=11
\newcount\xe@alloc@intercharclass % allocates intercharclass
\xe@alloc@intercharclass=\thr@@ % from 4 (1,2 and 3 are used by CJK, AFAIK)
\def\xe@alloc@#1#2#3#4#5{\global\advance#1\@ne
 \xe@ch@ck#1#4#2% make sure there's still room
 \allocationnumber#1%
 \global#3#5\allocationnumber
 \wlog{\string#5=\string#2\the\allocationnumber}}
\def\xe@ch@ck#1#2#3{%
 \ifnum#1<#2\else
  \errmessage{No room for a new #3}%
 \fi}
\def\newXeTeXintercharclass{%
 \xe@alloc@\xe@alloc@intercharclass\XeTeXintercharclass\chardef\@cclv} %at most 254
```
<!-- {% endraw %} -->

For LuaTeX, there are a couple of things in `lualatex.ini` that should be in the format. First, there is a difference in how this engine handles negative values of `\endlinechar` compared with other TeX engines. That requires a patch to LaTeX2e's `\@xtypein`. More importantly, LuaTeX only actives the extensions to TeX if some Lua code is used

```latex
\begingroup
\catcode`\{=1
\catcode`\}=2
\directlua{
  % etex and pdftex primitives are enabled without prefixing
  % as well as extented Unicode math primitives (see below)
  tex.enableprimitives('',
    tex.extraprimitives('etex', 'pdftex', 'umath'))
  % other primitives are prefixed with luatex (see below)
  tex.enableprimitives('luatex',
    tex.extraprimitives('core', 'omega', 'aleph', 'luatex'))
  }
\endgroup
```

This has to come right at the start of the build process, but is another thing that can sensibly go into `latex.ltx`. The team also wonder if all of the primitives should have their 'natural' names without the `luatex` prefix.

All of this can be added to `latex.ltx` without altering what users have available and without breaking LaTeX2e for pdfTeX users. The team have these changes made in the development version of the kernel. There are other things yet to be finalised, but it's highly likely the next release of the LaTeX2e kernel will (finally) recognise the Unicode engines and bring this stuff 'in house'.
