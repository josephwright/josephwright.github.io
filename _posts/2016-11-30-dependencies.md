---
title: Dependencies
layout: post
permalink: /2016/11/30/dependencies/
categories:
  - General
tags:
  - CTAN
  - packaging
---
There's been some [recent discussion](https://tug.org/pipermail/tex-live/2016-November/039434.html) on the [TeX Live mailing list](https://tug.org/mailman/listinfo/tex-live) about recording dependencies for (La)TeX packages. This is a good idea but means that package authors need to think about their dependency situation. So I thought a few words on this would be helpful, at least from the point of view of the most common case: LaTeX packages.

It's pretty easy to accumulate `\RequirePackage` lines in your source, but if you are serious about giving a useful set of dependencies you need to know what each one is for. In many ways the rule is easy: require each package you use. What makes that more complicated is that you might use features which are available when you load package X but are actually provided by package Y. For example, if you load my `siunitx` package, it loads `array` so means that you can do for example

```latex
\begin{tabular}{>{$}l<{$}}
```

So how do you tell what your 'real' dependencies are? The usual rule is that you check the documentation: does it say that package X itself provides the features you use? In the case above, `siunitx` doesn't document that syntax extension for `tabular`: it's documented by `array`. So if you wrote a package that uses `siunitx` but also needs to use features from `array` you should

```latex
\RequirePackage{array}
\RequirePackage{siunitx}
```

This means that even if at some future stage there's a change in the internals of a package you load, things should still all work.

If you want to track down where stuff might be coming from, you can always `\listfiles` to get a full overview of your current package use (starting from a small example).

There are a few places were packages are so closely linked you might not have to list them both. The most obvious is Ti<em>k</em>Z/`pgf`: the two are different 'layers' of the same set up but are documented together, so if you load Ti<em>k</em>Z you can assume `pgf`. Of course, there is no harm in listing both!
