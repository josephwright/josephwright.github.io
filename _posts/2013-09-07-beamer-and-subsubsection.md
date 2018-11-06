---
title: Beamer and \subsubsection
layout: post
permalink: /2013/09/07/beamer-and-subsubsection/
categories:
  - beamer
---
I'm hoping to address a few [bugs](https://bitbucket.org/rivanvx/beamer/issues?status=new&amp;status=open) in [`beamer`](https://ctan.org/pkg/beamer) over the next few days. One category that is always tricky is things linked to using `\subsubsection`. If you've read the `beamer` manual carefully, you'll know that the original author of the class really didn't want people to use `\subsubsection` in talks. However, he also didn't ban it entirely, leaving me with a tricky situation. The problem is that while `\subsubsection` works, many of the things you might expect to happen from the relationship between `\section` and `\subsection` fail with `\subsubsection`, and from the code that may well be 'by design'. Of course, I can change the 'rules', but `beamer` has been around a long time and it's also somewhat complex code. As such, I'm always having to make judgements on how to deal with these bugs. My advice: don't use `\subsubection` in `beamer` documents! Certainly don't be surprised if when you ignore that advice odd things happen.
