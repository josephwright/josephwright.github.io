---
title: LaTeX3&#58; More use, more work
layout: post
permalink: /2011/09/01/latex3-more-use-more-work/
categories:
  - LaTeX3
---
In the latest [LaTeX3 News](https://www.latex-project.org/site-news.html#2011-08-09), the [Project](https://www.latex-project.org/) announced that a [mirror of the development code](https://github.com/latex3/svn-mirror) is available on [GitHub](https://github.com/). Since then, there has been a definite increase in using expl3 (the LaTeX3 programming language), and we've had a number of very good questions on the LaTeX3 mailing list.

The programming layer of LaTeX3 works well in the main, and so it's very pleasing to see other people starting to pick up on using it. Of course, there are some rough edges, and one result of the questions is that these have to be addressed. At the same time, wider use means that there is a greater need to make sure that the code is stable enough. Getting the balance right between making desirable changes and ensuring that other peoples code does not break is not easy! So there is more work to do with greater use.

At the same time, there is the question of a wider 'road map'. For the programming layer, there are a few outstanding issues, for example a broader string module and an expandable floating point unit (both under way). However, most of the 'big issues' are outside of the base layer: we need support for a new format. There's quite a lot to talk about there, and I'll come back to it in another post in a day or so.
