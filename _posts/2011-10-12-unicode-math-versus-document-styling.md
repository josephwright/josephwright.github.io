---
title: Unicode math versus document styling
layout: post
permalink: /2011/10/12/unicode-math-versus-document-styling/
categories:
  - General
tags:
  - math mode
  - Unicode
---
There is a lot of work going on to develop methods for directly including mathematical meaning in documents. Projects such as [STIX](http://www.stixfonts.org/), [XITS](https://github.com/khaledhosny/xits-math) and [Latin Modern Math](http://www.gust.org.pl/projects/e-foundry/lm-math) are intended to provide a range of glyphs for mathematical use while retaining meaning by using the appropriate Unicode code point. Undoubtedly, this is a great idea for reusing information. However, there is always a pay-off, and in this case it is some awkwardness with document styling.

In a standard TeX math font, attributes such as bold or sans-serif can be switched on pretty easily, and also apply on an 'ongoing' basis. I make use of this in [`siunitx`](https://ctan.org/pkg/siunitx) to allow 'detection' of the local font conditions. Life is much more complex with Unicode maths fonts. Instead of something like bold being a casual attribute of a symbol, it's intrinsic to the symbol. So you can't simply switch from on bold, or sans-serif, or anything else.

For serious mathematicians, that probably makes good sense: they make a wide and complex use of the appearance of symbols to convey meaning. On the other hand, it's a bit awkward if you have a caption which is set in bold and want your simple piece of mathematics to match. I'm still thinking about the best way to handle this: suggestions are welcome!
