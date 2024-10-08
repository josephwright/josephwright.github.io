---
title: siunitx v2.4 beta
layout: post
permalink: /2011/11/09/siunitx-v2-4-beta/
categories:
  - Packages
  - siunitx
---
Development of the next release of [`siunitx`](http://ctan.org/pg/siunitx) has gone quite smoothly: I've added a few new features, and there is now nothing outstanding for v2.4. So it is time to ask for some volunteers to test the code.

In terms of new features, I have added the a [choice of rounding modes](https://github.com/josephwright/siunitx/issues/40) modes the ability to [compress down exponents in ranges and lists](https://github.com/josephwright/siunitx/issues/62), both long-standing feature requests. In response to a [recent TeX.sx question](https://tex.stackexchange.com/q/32925/73), `siunitx` can now also[ turn exponents into unit prefixes](https://github.com/josephwright/siunitx/issues/173). At a lower level, I've also altered some of the options internally so fewer of the assume math mode.

To test, please download the [ready to install TDS-style .zip](/uploads/2011/11/siunitx.tds_.zip) file and install it locally. You should then be good to go. Feedback as a [bug report](https://github.com/josephwright/siunitx/issues?q=is%3Aopen+is%3Aissue) or [by e-mail](mailto:joseph@texdev.net) welcome, as always. Assuming there are no problems, I'd expect to upload to [CTAN](https://www.ctan.org) by the end of the month.
