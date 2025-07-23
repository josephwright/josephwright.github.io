---
title: "biblatex: A team to continue the work"
layout: post
permalink: /2012/04/23/biblatex-a-team-to-continue-the-work/
categories:
  - biblatex
  - Packages
---
I [posted a while ago](/2012/04/03/biblatex-status/) about [`biblatex`](https://ctan.org/pkg/biblatex), looking for news of the author, Philipp Lehman. He'd been very active in replying to bug reports up to about 5 months ago, since when no-one has heard from him. As I said before, that's a big concern well beyond LaTeX work, but it's also left a question over continued development of `biblatex`.

Philipp Lehman had discussed a number of plans with the lead developer of [Biber](http://biblatex-biber.sourceforge.net/), Philip Kime. Unsurprisingly, Philip Kime has been keen to make sure that development of `biblatex` continues, but he wanted some help with the styles and any 'hard-core' TeX stuff. So a small team of '`biblatex` maintainers' has been set up:

- [Philip Kime](https://tex.stackexchange.com/users/1657/plk) (lead)
- [Audrey Boruvka](https://tex.stackexchange.com/users/4483/audrey)
- Me

We've got two separate tasks. First, we want to deal with issues with the current release of `biblatex` (v1.7). These are [tracked on the SourceForge site](http://sourceforge.net/tracker/?group_id=244752&atid=1126005), and there are a few outstanding which are being looked at. Second, we want to continue the work that Philipp Lehman had planned. That work is taking place on [GitHub](https://github.com/plk/biblatex/), and there are some big issues to tackle.

Perhaps the biggest single item on the horizon for `biblatex` 2.0 is dropping BibTeX support, and going Biber-only. That's something that Philipp Lehman has been planning for some time: the reality is that supporting BibTeX is increasingly awkward, and it's making adding new features increasingly complex (and bug-prone). Of course, dropping BibTeX support will be a significant change, but it's been on the horizon for some time, and will open the way to further extending the data model `biblatex` (and Biber) user.

Of course, if Philipp Lehman does return (and we hope he does), then the 'team' will be very happy to hand back to him. For the moment, sticking with the roadmap seems the best way forward.
