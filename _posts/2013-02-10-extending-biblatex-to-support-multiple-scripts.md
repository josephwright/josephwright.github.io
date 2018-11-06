---
id: 1596
title: Extending biblatex to support multiple scripts
date: 2013-02-10T11:45:09+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1596
permalink: /2013/02/10/extending-biblatex-to-support-multiple-scripts/
categories:
  - biblatex
  - Packages
tags:
  - xparse
---
As regular readers will know, I've taken an interest in [`biblatex`](https://ctan.org/pkg/biblatex) since it was first developed. Since the [original author disappeared](http://www.texdev.net/2012/04/03/biblatex-status/), I've been at least formally [involved in maintain the code](http://www.texdev.net/2012/04/23/biblatex-a-team-to-continue-the-work/). So far, that's been limited to tackling a few tricky low-level TeX issues, but there are some bigger issues to think about.

Philip Kime, lead Biber and `biblatex` developer, is keen to extend the LaTeX end to supporting multiple scripts. The Biber end is already done (in the 'burning edge' version), and writes to the `.bbl` file in the format:

<!-- {% raw %} -->
```latex
\field{form=original,lang=default}{labeltitle}{Title}
\list{form=original,lang=default}{location}{1}{%
  {Москва}%
}
\list{form=romanised,lang=default}{location}{1}{%
  {Moskva}%
}
```
<!-- {% endraw %} -->

However, that presents a big issue: how to do that without breaking every existing style. Supporting scripts means we need an additional argument for a very large number of commands: some of them need to have _two_ optional arguments, and some of them need to be expandable:

```latex
\iffieldundef[form=original,lang=default]{....}
```

Reading (two) optional arguments and working through keyval options expandably is tricky, which is where I come in. The natural way for me to solve the first problem is to use LaTeX3, and the [`xparse`](https://ctan.org/pkg/xparse) package. However, that's a big change for `biblatex`, so before I (and the rest of the `biblatex` team) go for this I though it would be worth raising the issue and looking for opinions. The alternative is to write the code into `biblatex` directly, but it's complicated and as I've already done the job once I'm reluctant to do this!

So, what I want to know is 'What do users think?' Is it reasonable to require `xparse` as part of `biblate
