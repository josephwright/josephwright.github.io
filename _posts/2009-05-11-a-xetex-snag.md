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
Testing the current <a title="LaTeX3 development code" href="http://www.latex-project.org/code.html">LaTeX3 code</a> means worrying about what primitives are available. Recent releases of <a title="pdfTeX" href="http://www.pdftex.org">pdfTeX</a> have included a number of new primitives, and the expl3 system currently uses <code>\pdfstrcmp</code> if it finds it. This has already caused one issue, as things were broken if it was not available. So I've been modifying the test system a little, to run the tests with pdfLaTeX and XeLaTeX. The “new” primitives are not available with <a title="The XeTeX typesetting system" href="http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&amp;id=XeTeX">XeTeX</a>, so this is a good test of our code: it's supposed to work with both. I've found one odd thing going on with the LateX3 code, but also one thing that seems to be a XeTeX snag.

The snag can be tracked down (thanks to Morten Høgholm) to a minimal case:
<pre>\message{\ifcat\par\relax T\else F\fi}</pre>
If you try this in TeX or pdfTeX, you get <code>T</code> in the log (as <em>The TeXbook</em> says you should). With XeTeX, you get <code>F</code>. Whether this is a bug or a feature, I don't know. I'm sure Jonathan Kew will elaborate, but it reminds me of the need to test using different set ups. You can imagine some very odd errors appearing with this type of thing!
