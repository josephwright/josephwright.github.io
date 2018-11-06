---
title: A roadmap for siunitx
layout: post
permalink: /2011/06/18/a-roadmap-for-siunitx/
categories:
  - Packages
  - siunitx
---
My [`siunitx`](https://ctan.org/pkg/siunitx) package continues to attract feature requests, even though for me and many people it is essentially ‘feature complete’. Many of these requests are as a result quite complex, and probably somewhat esoteric, but I do aim to be as accommodating as I can. At the same time, I want to avoid breaking things for the majority. So my approach is to take a few issues at a time and to work on them for each 2._x_ release, plus of course the regular bug fixes. At the same time, I'm keen to review my own work and to tighten up on some parts of the code. That's particularly important in adding new features, as there are places where it turns out a bit more structure is needed.

For version 2.3, I'm focussing on the mechanics of tabular alignment. This entire part (around 1500 lines of code) is going to be rewritten, hopefully making things more reliable, improving performance and also ease of maintenance. For version 2.4, I'll probably look again at how tablular material is collected up by siunitx,  and also at the parser for numbers: I've had some ideas to improve performance. Beyond that, I have a few general thoughts, for example the idea of '[multiple error](https://github.com/josephwright/siunitx/issues/24)' parsing: that looks tricky!

Anther area to work on is the option interface. Some of these are not perfect, and v2.3 will see some revisions. I have further revisions already in mind, but don't want to do too much at once so again have some ideas for v2.4. At the same time, I think there are some performance enhancements available by recoding parts of the option system. I'll be doing that as part of the general review, and so again we should see evolution in that area. I'll return to this general issue in another post.

That is quite a list, and so I'll certainly be kept busy. I have other things to do as well, both in the TeX world and outside, so at the moment my thinking is v2.3 in July, with v2.4 in the autumn (perhaps October or November) and v2.5 vaguely pencilled in for ‘first half of 2012’. Hopefully that will keep everyone happy.
