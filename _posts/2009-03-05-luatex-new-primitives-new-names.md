---
title: "LuaTeX: new primitives, new names"
layout: post
permalink: /2009/03/05/luatex-new-primitives-new-names/
categories:
  - General
tags:
  - LuaTeX
  - XeTeX
---
There has been quite a bit of discussion recently on the [LuaTeX mailing list](https://tug.org/pipermail/luatex/) about primitive names.  The basic set of primitive names provided by TeX has already been extended by e-TeX, [pdfTeX](https://tug.org/applications/pdftex/) and [XeTeX](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=xetex). While e-TeX primitives have names which express only the function (such as `\detokenize`), both pdfTeX and XeTeX have tended to add the engine name to all new primitives. So for example pdfTeX provides the `\pdfprimitive` function, which always carries out the original function of a name, even if it has later been redefined:

```latex
\let\everypar\undefined
% \everypar{Some stuff} % Gives an error
\pdfprimitive\everypar{Some stuff}
```

will, for example, add material to `\everypar` despite the redefinition.

In [LuaTeX](http://www.luatex.org/), the idea of adding an engine-specific prefix has been abandoned. The example above shows one reason why: `\pdfprimitive` makes more sense with the name `\primitive` (which is what LuaTeX calls it). The problem with this is that name clashes are marginally more likely without a prefix (for example, `\expanded` is used in [ConTeXt](http://wiki.contextgarden.net/Main_Page) as a macro, but this is planned as a primitive for pdfTeX 1.50).

On the other hand, LuaTeX is a fundamental break with previous engines, as the internal changes mean that it may give different line breaks and so on to earlier systems. Thus the argument for new, logical, primitive names is that moving to LuaTeX is not the same as moving from TeX to pdfTeX or pdfTeX to XeTeX. There will be changes, and the user (or package developer) will need to think about them before diving in.

Overall, I think the LuaTeX idea is the best in the long term. Primitives which have well specified names help everyone, and some times change is necessary. I'll be interest to see if the `\directlua` primitive for actually using Lua ends up with a shorter name (just `\lua`, anyone?).
