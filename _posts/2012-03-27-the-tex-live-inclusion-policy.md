---
title: The TeX Live inclusion policy
layout: post
permalink: /2012/03/27/the-tex-live-inclusion-policy/
categories:
  - General
tags:
  - TeX Live
---
[TeX Live](https://tug.org/texlive/) takes almost all of the material it includes from [CTAN](http://ctan.org/), but not everything that goes to CTAN gets into TeX Live. That's because CTAN will take anything TeX-related, but TeX Live is 'free as in speech' and that means that some things are not suitable for inclusion.

Packages are removed from time to time license reasons: they are not actually free, so can't stay. However,  a few packages have been removed from TeX Live they did not fit in with the policy for inclusion in TeX Live for other reasons. That has caused a bit more surprise, and some [questions have come up about it](https://tex.stackexchange.com/questions/49479/package-flashmovie-removed-from-tex-live/49482#49482).So I thought it would be useful to summarise the TeX Live situation as I understand it.

The clearest case is material where the license is not 'free' (as defined by [Debian](http://www.debian.org/)): anything without a free license cannot go into TeX Live. Perhaps the next clearest case is support for commercial fonts. To use a font with pdfLaTeX, it's necessary to have the correct support files. Quite often, these are sent to CTAN with a free license, but don't go into TeX Live. Without the fonts themselves you can't use the support material, so it's only practically useful if you are happy to buy the non-free fonts.

Life is more complicated in the cases that have come up recently, where things are less clear cut. As many readers will know, the PDF specification is [nowadays an ISO standard](http://www.iso.org/iso/pressrelease.htm?refid=Ref1141), and there are several PDF viewer implementations with free licenses. However, there are two caveats to this. First, Adobe have published extensions to the ISO version of the PDF specification. Secondly, creating a PDF viewer does not mean that every possible PDF feature is implemented. Why is this relevant to TeX Live? Well, there are several packages on CTAN, for example [`media9`](https://ctan.org/pkg/media9), which use PDF features which are either not part of the ISO standard PDF specification or which are only available in Adobe Reader. These have been removed from TeX Live as the conclusion is that they only have real functionality along with a non-free product. (There seems to be some confusion as to whether any of the free viewers may support at least some of the necessary PDF features: I can't find a definite answer.)

That judgement is complicated: this case is not the same as the font situation. The PDFs produced by for
example `media9` are still viewable with free readers, they just don't have all of the bells and whistles available. It's also the case that if we look back in time a little, PDFs were only viewable using Adobe Reader, but that did not stop the development of  [pdfTeX](http://www.pdftex.org/), [`hyperref`](https://ctan.org/pkg/hyperref) and so on. On the other hand, the TeX Live developers already do a great deal of hard work, and it's not unreasonable for them to set a policy that they are comfortable with: after all, it's a labour of love. I think that the policy is reasonably clear, although tracking what is practically implemented, as opposed to what is legally allowed, is rather likely to change over time.
