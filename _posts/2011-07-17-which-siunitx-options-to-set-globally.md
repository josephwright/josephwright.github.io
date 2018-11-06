---
id: 1048
title: Which siunitx options to set globally?
date: 2011-07-17T16:08:14+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1048
permalink: /2011/07/17/which-siunitx-options-to-set-globally/
categories:
  - Packages
  - siunitx
---
On the <a href="http://tex.stackexchange.com/">TeX.SX</a> site recently, there was some discussion about <a href="http://tex.stackexchange.com/q/23193/73">locally over-riding the <code>round-mode = places</code> setting</a> in my <a title="A comprehensive (SI) units package" href="http://ctan.org/pkg/siunitx">siunitx</a> package. One thing this highlights for me is the need to think about which settings to apply globally.

Some siunitx settings are about consistency of appearance, and seem to apply naturally to entire documents. A classic example would be <code>output-decimal-marker</code>: if you are using <code>,</code> as a decimal marker, it should apply everywhere!

However, this is not so clear-cut for many of the options related to number-manipulation. The rounding options in particular are really intended for the case where you have some auto-generated data (say a long list from an instrument), and the real accuracy is not as great as the apparent precision. Instruments are great at providing lots of numbers, but it takes a bit of human thought to decide how many of these are really relevant. So for these cases, setting an appropriate rounding scheme is perfectly sensible.

On the other hand, for a number you've typed in yourself I'd hope that you've done the thinking part when the number is typed, so rounding by the computer is not needed. That suggests to me that most of the time rounding should not be set as a global option.

Of course, it will depend on the exact nature of the document in question. If all of the data in a document is in tables, all of which need rounding, then there is a performance gain from setting the rounding once globally. So the best I can say, guidance-wise, is ‘think about <em>your</em> document’!
