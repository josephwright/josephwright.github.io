---
id: 1617
title: Moving from Mercurial to Git
date: 2013-04-25T09:08:49+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1617
permalink: /2013/04/25/moving-from-mercurial-to-git/
categories:
  - General
tags:
  - BitBucket
  - Git
  - github
  - Mercurial
  - Version control
---
Over the years of working with LaTeX, I've picked up a bit about version control systems for code: this post is more about general programming than TeX.

I started out with [Subversion](http://subversion.tigris.org/), then moved to [Mercurial](http://mercurial.selenic.com/) when I got involved in [`beamer`](https://ctan.org/pkg/beamer) maintenance. The idea is the same whatever system you are using: by keeping a track of changes in the code you help yourself in the long term, and make it easier for other people to help too. Mercurial is one of several 'distributed' version control systems (DCVS) that have been developed over the last few years. The idea is that each 'repository' (copy of the code) has the history with it, and so is independent of any server. You can still send your changes to a server, and that is very popular, but you don't have to. Sending code to a public server makes it easy to let other people get involved, report issues and so on, and there are lots of sites that will help you do this.

I picked Mercurial over the other leader, [Git](http://git-scm.com/), mainly because the other guy involved in looking after `beamer` went this way and put the code on [BitBucket](https://bitbucket.org/). At the time, BitBucket did Mercurial while [GitHub](https://github.com/) did Git. BitBucket changed hands a little while ago now, and they brought in Git support. They've now moved to make Git the 'standard' repository type. That tells me that Git is likely to 'win' as the most popular DCVS (it's looked that way for a while), and so it's time to reconsider my use of Mercurial.

It turns out that moving from Mercurial to Git is pretty easy: there is a script called [`fast-export`](https://github.com/frej/fast-export) that does the job. Converting the code itself is therefore easy: run the script (you need a Unix system, so on Windows I'm using a virtual [Ubuntu](http://www.ubuntu.com/) machine with [VirtualBox](https://www.virtualbox.org/)). Life gets a bit more interesting, though, if you want to keep your issues database. BitBucket does offer issue import and export, but no easy way to convert from Mercurial to Git. At the same time, the way that the two systems refer to individual commits means that if you don't edit your issues, any links to the commits will be messed up. That means that its as easy to move to GitHub as it is to stay on BitBucket. So that's what I've decided to do (GitHub is pretty popular with other LaTeX developers). I'm working through my repositories, converting to Git and uploading to GitHub, then copying the issue information by hand and doing minor edits. That includes making sure that I keep the links which show how I fixed things. Apart from [`siunitx`](https://ctan.org/pkg/siunitx), my packages don't have a lot of issues (no more than a dozen each), so I can do that by hand without too much work. I'd a bit surprised no-one has written a script to do this, but at least it will not take too long. I'd expect everything except `siunitx` to be moved by the weekend, and even this 'big job' to be done within a couple of weeks.
