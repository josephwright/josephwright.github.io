---
id: 1174
title: siunitx v2.4 beta
date: 2011-11-09T18:49:10+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1174
permalink: /2011/11/09/siunitx-v2-4-beta/
categories:
  - Packages
  - siunitx
---
Development of the next release of <a href="http://ctan.org/pg/siunitx">siunitx</a> has gone quite smoothly: I've added a few new features, and there is now nothing outstanding for v2.4. So it is time to ask for some volunteers to test the code.

In terms of new features, I have added the a <a href="https://bitbucket.org/josephwright/siunitx/issue/40/choice-of-methods-for-rounding-exactly">choice of rounding modes</a> modes the ability to <a href="https://bitbucket.org/josephwright/siunitx/issue/62/more-possibilities-for-the-sirange-and">compress down exponents in ranges and lists</a>, both long-standing feature requests. In response to a <a href="http://tex.stackexchange.com/q/32925/73">recent TeX.sx question</a>, siunitx can now also<a href="https://bitbucket.org/josephwright/siunitx/issue/173/convert-scientific-notation-to-si-prefix"> turn exponents into unit prefixes</a>. At a lower level, I've also altered some of the options internally so fewer of the assume math mode.

To test, please download the <a href="http://www.texdev.net/wp-content/uploads/2011/11/siunitx.tds_.zip">ready to install TDS-style .zip</a> file and install it locally. You should then be good to go. Feedback as a <a href="https://bitbucket.org/josephwright/siunitx/issues?status=new&amp;status=open">bug report</a> or <a href="mailto:joseph.wright@morningstar2.co.uk">by e-mail</a> welcome, as always. Assuming there are no problems, I'd expect to upload to <a href="http://www.ctan.org/">CTAN</a> by the end of the month.
