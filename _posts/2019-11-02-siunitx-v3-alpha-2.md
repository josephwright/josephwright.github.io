---
title: siunitx v3 alpha 2
layout: post
permalink: /2019/11/02/siunitx-v3-alpha-2
categories:
  - siunitx
---

I've been talking about a new version of
[`siunitx`](https://ctan.org/pkg/siunitx) for a
[number of years now](/2014/03/13/work-on-siunitx-v3/), and progress has been
slower than I'd hoped.

After something of a hiatus (I
[released the first alpha last year](/2018/07/21/tug2018-day-two/)),
I've been back looking at the code again and expanding the range of tests
to try to pick up more of the hidden bugs. I'm hoping now to have a reasonably
regular alpha series as I build toward a first feature-complete beta,
probably by the Spring.

Taking advantage of the possibilities offered by [GitHub](https://github.com)
and [Travis-CI](https://travis-ci.com), I've decided to place the zip
files there rather than upload them here to my blog. (To be fair, the blog
itself is currently hosted by GitHub too!)

The work on version 3 is taking place throughout the codebase, but the
differences between the first and second alpha versions are focussed in
two areas

- Testing the backward-compatibility options
- Beginning to implement quantities

There are still a lot of features to add, but for me the code works as
a user. Of course, I don't use most of the features!

One thing that's definitely _not_ done is full compatibility with version
2 font features. At the moment, I feel I'll end up providing a way to
continue to load v2 'behind the scenes' for people who need it: I've
got a completely new approach to font control, and it's not really
possible to map readily between old and new options. Probably I will have
more on this for alpha 3, but at present I'd love feedback on any font
cases that don't work with the new approach.

One area I'd like to highlight is performance. I've always said that the
move from v1 to v2 (using [`expl3`](https://ctan.org/pkg/l3kernel)) led to
a bit performance jump. I've now got some figures, which also show v3 is
going to be even better. My test document, using
[l3benchmark](https://ctan.org/pkg/l3experimental) of course, is

```latex
\RequirePackage{latexrelease}[2019-10-01]
\documentclass{article}
\usepackage{expl3}
\usepackage{l3benchmark}
\usepackage{siunitx}
\listfiles
\ExplSyntaxOn
\cs_new_eq:NN \benchmark \benchmark:n
\ExplSyntaxOff
\begin{document}
\benchmark{\SI{0.234e3}{\joule\per\mole\per\kelvin} }
\end{document}
```

 which gives

 ```
Version 1 0.0155 seconds (4.42e4 ops)
Version 2 0.00415 seconds (1.46e4 ops)
Version 3 0.00195 seconds (7.14e3 ops)
 ```
