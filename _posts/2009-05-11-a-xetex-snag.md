---
id: 287
title: A XeTeX snag
date: 2009-05-11T16:55:29+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=287
permalink: /2009/05/11/a-xetex-snag/
categories:
  - LaTeX3
tags:
  - XeTeX
---
Testing the current [LaTeX3 code](https://www.latex-project.org/code.html) means worrying about what primitives are available. Recent releases of [pdfTeX](http://www.pdftex.org) have included a number of new primitives, and the expl3 system currently uses `\pdfstrcmp` if it finds it. This has already caused one issue, as things were broken if it was not available. So I've been modifying the test system a little, to run the tests with pdfLaTeX and XeLaTeX. The “new” primitives are not available with [XeTeX](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=XeTeX), so this is a good test of our code: it's supposed to work with both. I've found one odd thing going on with the LateX3 code, but also one thing that seems to be a XeTeX snag.

The snag can be tracked down (thanks to Morten Høgholm) to a minimal case:

```latex
\message{\ifcat\par\relax T\else F\fi}
```

If you try this in TeX or pdfTeX, you get `T` in the log (as _The TeXbook_ says you should). With XeTeX, you get `F`. Whether this is a bug or a feature, I don't know. I'm sure Jonathan Kew will elaborate, but it reminds me of the need to test using different set ups. You can imagine some very odd errors appearing with this type of thing!
