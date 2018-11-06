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
Development of the next release of [siunitx](http://ctan.org/pg/siunitx) has gone quite smoothly: I've added a few new features, and there is now nothing outstanding for v2.4. So it is time to ask for some volunteers to test the code.

In terms of new features, I have added the a [choice of rounding modes](https://bitbucket.org/josephwright/siunitx/issue/40/choice-of-methods-for-rounding-exactly) modes the ability to [compress down exponents in ranges and lists](https://bitbucket.org/josephwright/siunitx/issue/62/more-possibilities-for-the-sirange-and), both long-standing feature requests. In response to a [recent TeX.sx question](http://tex.stackexchange.com/q/32925/73), siunitx can now also[ turn exponents into unit prefixes](https://bitbucket.org/josephwright/siunitx/issue/173/convert-scientific-notation-to-si-prefix). At a lower level, I've also altered some of the options internally so fewer of the assume math mode.

To test, please download the [ready to install TDS-style .zip](/wp-content/uploads/2011/11/siunitx.tds_.zip) file and install it locally. You should then be good to go. Feedback as a [bug report](https://bitbucket.org/josephwright/siunitx/issues?status=new&amp;status=open) or [by e-mail](mailto:joseph.wright@morningstar2.co.uk) welcome, as always. Assuming there are no problems, I'd expect to upload to [CTAN](https://www.ctan.org) by the end of the month.
