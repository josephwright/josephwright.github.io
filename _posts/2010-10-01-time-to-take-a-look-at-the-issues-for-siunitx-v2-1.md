---
id: 815
title: Time to take a look at the issues for siunitx v2.1
date: 2010-10-01T21:30:28+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=815
permalink: /2010/10/01/time-to-take-a-look-at-the-issues-for-siunitx-v2-1/
categories:
  - Packages
  - siunitx
---
The [list of issues](http://bitbucket.org/josephwright/siunitx/issues?status=new&amp;status=open) for [siunitx](https://ctan.org/pkg/siunitx) has been growing for a while. I've been holding off work on the bigger issues while bugs in v2.0 have come up, as I'd prefer to have something that works for most people now rather than try to add more new features too soon. At the same time, I'm also busy working on [other things](http://www.latex-project.org/latex3.html). However, I've been prodded by a few users to make a start on some of the feature requests. I do aim to please, so I'm going to make a start on the list.

Of course, just because I look at something does not mean I'll do it. I decided to start simple, and took a look at [issue 71](http://bitbucket.org/josephwright/siunitx/issue/71/kerning-of-femto-prefix). The question here was about automatically adding kerning for things like `\femto\farad`, as the kerning in Computer Modern is not good here. I did write some code, but looking at it decided that this is too close to the font choice for me. So I've closed the issue as 'WONTFIX'. I'll see whether this sticks or whether there is a lot of demand for such a feature.

The plan is to get on with adding features and fixing more complex issues over the next few weeks. I never leave the code unusable (I use the development version as my day-to-day workhorse), so you can grab the .dtx file and try things out if you like. I'll post again if there are any particular new features or changes that need a try out.
