---
title: siunitx version 2.0&#58; alpha 1
layout: post
permalink: /2010/01/31/siunitx-version-2-0-alpha-1/
categories:
  - Packages
  - siunitx
tags:
  - alpha
  - snapshot
---
I've been working on [`siunitx`](https://ctan.org/pkg/siunitx) version 2, getting the code to the point where I'd hope it works for most things that the current release does. Over the last couple of weeks I hope I've sorted out the table issues which tend to be a problem in version 1, plus 'mopped up' a few outstanding odds and ends. So it feels like an appropriate point for a public snap shot of the code. As progress has been good, I'm calling this one alpha 1.

At this stage, there are likely to be some bugs and other annoyances in the code. However, I hope that enough works for people to risk taking the plunge and trying it out. For those willing to try out `siunitx` v2.0, you can get:

- [The ready to install TDS-style zip file](/wp-content/uploads/2010/01/siunitx.tds_1.zip)
- [The package documentation](/wp-content/uploads/2010/01/siunitx.pdf)
- The source file (dtx)

You'll need to have up to date installations of both [`expl3`](https://ctan.org/pkg/expl3) and the [`xpackages`](https://ctan.org/pkg/xpackages) to try out  the code, as internally the new code uses the [LaTeX3](https://www.latex-project.org/latex3.html) internal syntax. The biggest change that users should see from version 1 is that I've re-thought the option names. They are mainly longer, but more informative, in the new code. Improvements to the names I've picked are of course welcome.

At this stage, I'm still working on adding more ideas to the code. So there are some omissions in the release that I know are there and am intending to sort out. Of course, different users have different priorities for improvement. That said, there are bound to be things which simply are broken, things I've forgotten and the odd item that I'm currently planning not to carry forward from version 1. Feedback by as comments here, by [e-mail](mailto:joseph.wright@morningstar2.co.uk) or at the BerliOS site, with a full release currently in my mind for June or July. Exactly how this will work out depends on other projects: I'd like, for example, to have some floating-point tools in `siunitx`, but for that I need to write them for LaTeX3. The feature list for the release certainly isn't fixed, and I'd expect that once v2.0 is out there will continue to be more ideas to add on.
