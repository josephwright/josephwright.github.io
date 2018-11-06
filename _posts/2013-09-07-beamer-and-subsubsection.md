---
id: 1644
title: Beamer and \subsubsection
date: 2013-09-07T17:03:32+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1644
permalink: /2013/09/07/beamer-and-subsubsection/
categories:
  - beamer
---
I'm hoping to address a few <a href="https://bitbucket.org/rivanvx/beamer/issues?status=new&amp;status=open">bugs</a> in <a href="http://ctan.org/pkg/beamer"><code>beamer</code></a> over the next few days. One category that is always tricky is things linked to using <code>\subsubsection</code>. If you've read the <code>beamer</code> manual carefully, you'll know that the original author of the class really didn't want people to use <code>\subsubsection</code> in talks. However, he also didn't ban it entirely, leaving me with a tricky situation. The problem is that while <code>\subsubsection</code> works, many of the things you might expect to happen from the relationship between <code>\section</code> and <code>\subsection</code> fail with <code>\subsubsection</code>, and from the code that may well be 'by design'. Of course, I can change the 'rules', but <code>beamer</code> has been around a long time and it's also somewhat complex code. As such, I'm always having to make judgements on how to deal with these bugs. My advice: don't use <code>\subsubection</code> in <code>beamer</code> documents! Certainly don't be surprised if when you ignore that advice odd things happen.
