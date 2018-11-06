---
id: 1673
title: beamer development
date: 2014-01-27T22:05:50+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1673
permalink: /2014/01/27/beamer-development/
categories:
  - beamer
---
As many readers will know, I'm a member of the two-man team in charge of maintaining the <a href="http://ctan.org/pkg/beamer"><code>beamer</code></a> class (the other team member is <a href="https://bitbucket.org/rivanvx">Vedran Miletić</a>). Vedran and I took over looking after <code>beamer</code> when it was unmaintained and some important bugs cropped up: lots of people rely on it, so fixes were important. There was a <a href="http://tex.stackexchange.com/q/155923/73">question on the TeX Stackexchange site recently</a> asking about the status of maintenance. It's a tricky one to tackle in a Q&amp;A, but it does make a good topic for the blog!

Vedran and I are committed to keeping <code>beamer</code> working, and that means fixing bugs as and when we can. At the same time, we are not likely to add much in the way of new feature: small changes over time only. There are a few reasons for that, the single biggest one of which is stability. The <code>beamer</code> class is very widely used, and does a lot of stuff. Making significant changes is therefore tricky, particularly as we don't have any automated tests. The internal <code>beamer</code> structure contributes a bit here: it's a complex set up, partly due to some issues in LaTeX2e (why I work on LaTeX3), partly because it has to be and partly as an 'overhaul' might have been useful at some stage. (It's far too late for the latter idea now: any big change would break too many documents.)

The second issue is of course time: both Vedran and I are busy, in my case not only with 'real life' but also with other (La)TeX projects! Then of course there is trying to stick to what <code>beamer</code> does: the original design quite deliberately doesn't do some things, so as 'auto-flowing' text.

If you watch the <a href="https://bitbucket.org/rivanvx/beamer/wiki/Home">BitBucket site for <code>beamer</code> development,</a> you will see changes, both to fix bugs and (slowly) add new features. That's not about to change: small changes, 'little and (relatively) often', are the order of the day here. Of course, if you have a patch you really want applying, we are always happy to take a look!
