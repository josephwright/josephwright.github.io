---
title: "Engine news from the LaTeX Project"
layout: post
permalink: /2024/11/05/engine-news-from-the-latex-project
categories:
  - General
---

The latest release of LaTeX went to [CTAN](https://ctan.org) on Friday, and
moves us forward in truly automatic tagging for PDFs, particularly for
mathematics. As part of the work, we have been looking at the capabilities of
different engines. Here, I want to summarise what users should take from that
for existing and for new documents.

## LuaTeX

LuaTeX offers the widest range of features, including the ability to access the
node list as it's constructed. We can use that to generate MathML automatically
for math mode fragments. If also allows us to do tagging in fewer passes than
in other engines and offers support for larger documents (due to dynamic memory
allocation). As such, LuaTeX is _the_ recommended engine for all new documents.

Work is continuing on adjusting parts of the setup to improve automation here:
for the present, you should be using
```latex
\usepackage{unicode-math}
```
to get the best results for math mode.

## XeTeX

The situation with XeTeX contrasts strongly with LuaTeX: although both are
Unicode engines, XeTeX has none of the flexibility available in LuaTeX. There
are significant technical limitations which mean that XeTeX cannot create
accessible PDFs at all: this is unlikely to change. The engine itself is
unmaintained, and with no access to internals, fixing the current issues alone
would not really help. XeTeX does not produce PDFs directly, and that
essentially rules out full tagging support (see below).

All of this means it is time to move away from XeTeX: certainly for new
documents, and even for existing ones. Users should look at alternative
approaches here, even if it means some source changes. This is most obvious for
users of [`xeCJK`](https://ctan.org/pkg/xecjk), who will need to look at the
methods offered by [`luatexja`](https://ctan.org/pkg/luatexja) instead: whilst
the latter is described as for Japanese, the underlying mechanisms should be
suitable for other East Asian languages.

## pdfTeX

pdfTeX is widely used as it is superbly stable and fast, at least if you are
dealing with languages where an 8-bit approach works. There are as a result a
vast body of existing LaTeX documents which rely on pdfTeX. As such, the LaTeX
Project are working to produce fully tagged PDFs from these sources, although
we cannot do quite the same job as with LuaTeX.

For new documents, moving to LuaTeX is the recommended approach: it will
continue to offer the most complete tagging support. For existing documents,
tagging is available and we hope to improve it further: this may eventually use
a LuaTeX-based approach emulating 8-bit approaches. At present, however,
tagging in pdfTeX is more limited than in LuaTeX.

## Other engines

There are other engines, most notable (u)pTeX. Like XeTeX, these do not
generate PDF directly, so may well be more limited in tagging support. Unlike
XeTeX, other engines do have (small) support teams and so may see developments
that help with tagging. However, the LaTeX Project team do not test these
engines, and so where possible a move to LuaTeX is suggested.
 
## Conclusions

The time to move to LuaTeX for new LaTeX documents is here. For existing pdfTeX
sources, tagging will be available, although it may be more limited than for
LuaTeX. pdfTeX users can keep their existing sources and will see tagging
available. XeTeX users really do need to re-work their sources for LuaTeX.
