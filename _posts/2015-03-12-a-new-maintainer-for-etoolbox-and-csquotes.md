---
title: A new maintainer for etoolbox (and csquotes)
layout: post
permalink: /2015/03/12/a-new-maintainer-for-etoolbox-and-csquotes/
categories:
  - Packages
tags:
  - csquotes
  - etoolbox
---
One of the most significant new LaTeX packages of recent years has been [`biblatex`](https://ctan.org/pkg/biblatex), originally developed by Philipp Lehman and offering an extremely powerful approach to bibliographies. As I've [covered before](/2012/04/03/biblatex-status/), Philipp Lehman vanished from the TeX world a few years ago. To keep `biblatex` development going, a [team was assembled](/2012/04/23/biblatex-a-team-to-continue-the-work/) led by Philip Kime. However, Philipp Lehman's other packages have up to now been left unmaintained.

The LaTeX team are [currently working on some LaTeX2e improvements](/2014/12/28/fixing-latex2e/), and they have a knock-on effect on Philipp Lehman's [`etoolbox`](https://ctan.org/pkg/etoolbox) package. To date, it's automatically loaded [`etex`](https://ctan.org/pkg/etex-pkg), but the team are moving that functionality to the LaTeX kernel so it will no longer be needed. Thus we needed to sort out a minor update to `etoolbox`. As I'm already involved with `biblatex`, it seemed natural for me to take up this challenge. I've therefore forked `etoolbox` (see [The LPPL: ‘maintainer’ or ‘author-maintained’](/2012/05/04/the-lppl-maintainer-or-author-maintained/) for why it's technically a fork), set up a [GitHub site](https://github.com/josephwright/etoolbox) and made the changes. Of course, two days after that 'one off' fix I got my first bug report!

Philipp Lehman's other big contribution along with `biblatex` and `etoolbox` is [`csquotes`](https://ctan.org/pkg/csquotes). While I don't have any immediate need to make a change there, this seems like a good time for someone to pick it up too. So I've set up a (technical) fork and [GitHub page](https://github.com/josephwright/csquotes) for that too, and expect to have a few minor changes to make (I've had informal discussions about at least one). Should there be a need I'll also be looking at Philipp's other packages (he and I had interesting discussions about [`logreq`](https://ctan.org/pkg/logreq), for example, and how the ideas might make it into `expl3`).
