---
id: 1800
title: A new maintainer for etoolbox (and csquotes)
date: 2015-03-12T22:01:10+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1800
permalink: /2015/03/12/a-new-maintainer-for-etoolbox-and-csquotes/
categories:
  - Packages
tags:
  - csquotes
  - etoolbox
---
One of the most significant new LaTeX packages of recent years has been <a href="http://ctan.org/pkg/biblatex"><code>biblatex</code></a>, originally developed by Philipp Lehman and offering an extremely powerful approach to bibliographies. As I've <a href="http://www.texdev.net/2012/04/03/biblatex-status/">covered before</a>, Philipp Lehman vanished from the TeX world a few years ago. To keep <code>biblatex</code> development going, a <a href="http://www.texdev.net/2012/04/23/biblatex-a-team-to-continue-the-work/">team was assembled</a> led by Philip Kime. However, Philipp Lehman's other packages have up to now been left unmaintained.

The LaTeX team are <a href="http://www.texdev.net/2014/12/28/fixing-latex2e/">currently working on some LaTeX2e improvements</a>, and they have a knock-on effect on Philipp Lehman's <a href="http://ctan.org/pkg/etoolbox"><code>etoolbox</code></a> package. To date, it's automatically loaded <a href="http://ctan.org/pkg/etex-pkg"><code>etex</code></a>, but the team are moving that functionality to the LaTeX kernel so it will no longer be needed. Thus we needed to sort out a minor update to <code>etoolbox</code>. As I'm already involved with <code>biblatex</code>, it seemed natural for me to take up this challenge. I've therefore forked <code>etoolbox</code> (see <a href="http://www.texdev.net/2012/05/04/the-lppl-maintainer-or-author-maintained/">The LPPL: ‘maintainer’ or ‘author-maintained’</a> for why it's technically a fork), set up a <a href="https://github.com/josephwright/etoolbox">GitHub site</a> and made the changes. Of course, two days after that 'one off' fix I got my first bug report!

Philipp Lehman's other big contribution along with <code>biblatex</code> and <code>etoolbox</code> is <a href="http://ctan.org/pkg/csquotes"><code>csquotes</code></a>. While I don't have any immediate need to make a change there, this seems like a good time for someone to pick it up too. So I've set up a (technical) fork and <a href="https://github.com/josephwright/csquotes">GitHub page</a> for that too, and expect to have a few minor changes to make (I've had informal discussions about at least one). Should there be a need I'll also be looking at Philipp's other packages (he and I had interesting discussions about <a href="http://ctan.org/pkg/logreq"><code>logreq</code></a>, for example, and how the ideas might make it into <code>expl3</code>).
