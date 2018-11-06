---
id: 1006
title: siunitx v2.2 released
date: 2011-04-14T08:24:54+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1006
permalink: /2011/04/14/siunitx-v2-2-released/
categories:
  - Packages
  - siunitx
---
As I [detailed a little while ago](http://www.texdev.net/2011/03/20/sorting-issues-for-consideration-for-siunitx-v2-2/), I've been working on v2.2 of [siunitx](https://ctan.org/pkg/siunitx). I've now released the latest version, v2.2, to [CTAN](https://www.ctan.org). There are a number of small changes, introducing new features, but I thought I would highlight a few.

A long-standing feature request has been to be able to use the [cancel](https://ctan.org/pkg/cancel) package to show how units cancel out. This is useful for teaching, although it's not of course part of the usual typesetting of units for publication. It turns out not to be too hard to allow this, so that you can now use input such as

```latex
\si[per-mode = fraction]{\cancel\kg\m\per\s\cancel\kg}
```

and have it come out properly. At the same time, I've made it possible to highlight particular units

```latex
\si{\highlight{green}\square\metre\candela\second}
```

again for teaching-related purposes.

A second long-standing request is to be able to parse uncertainties given in the form

```latex
\num{1.23 +- 0.15}
```

which was something more of challenge, but again is now working properly. So you can get the same output from the above and from

```latex
\num{1.23(15)}.
```

A final highlight is the new `\tablenum` macro. This is needed for aligning numbers inside `\multicolumn` and `\multirow`, which otherwise does not work. (At a technical level, both `\multicolumn` and `\mutirow` use the `\omit` primitive, and so the code inserted by the `S` column is not used. The `\tablenum` macro effectively makes the same approach available as a stand-alone function.)
