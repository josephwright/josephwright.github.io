---
title: LaTeX2e kernel development moves to GitHub
layout: post
permalink: /2017/12/16/latex2e-kernel-development-moves-to-github/
categories:
  - General
tags:
  - Git
  - github
  - issues
  - LaTeX2e
---
The [LaTeX team](https://www.latex-project.org) have two big jobs to do: maintaining LaTeX2e and working on LaTeX3 (currently as new packages on top of LaTeX2e). For quite a while now the LaTeX3 code has been [available on GitHub](https://github.com/latex3/latex3) as a mirror of the master repository. At the same time, the core LaTeX2e code was also available publicly using Subversion (SVN) _via_ the team website. At least in the web view, the latter has always been a bit 'Spartan', both in appearance and in features (only the most recent revision could be seen).

Coupled to viewing the code for any project is tracking the issues. For LaTeX2e, the team have used [GNATS](https://www.gnu.org/software/gnats/) for over twenty years. GNATS has served the team well, but like the web view is Subversion is showing its age.

We've now decided that the time is right to make a change. Eagle-eyed users will already have spotted the new [LaTeX2e GitHub page](https://github.com/latex3/latex2e), which is now _the_ master repo for the LaTeX kernel. We've not yet frozen the existing [GNATS database](https://www.latex-project.org/cgi-bin/ltxbugs2html?introduction=yes&amp;state=open), but new bugs should be reported [on GitHub](https://github.com/latex3/latex2e/issues). (For technical reasons, the existing GNATS bugs list is unlikely to be migrated to GitHub.)

Frank Mittelbach (LaTeX team lead developer) has written a short article on the new approach, which will be appearing in [_TUGboat_](https://tug.org/tugboat) soon. As Frank says, we hope that most users don't run into bugs in the kernel (it is pretty stable and the code has been pushed pretty hard over the years), but this new approach will make reporting that bit easier and clearer.

Accompanying the move of LaTeX2e to GitHub, the LaTeX3 Subversion repository has also been retired: the master location for this is also now [on GitHub](https://github.com/latex3/latex3). So everything is in a sense 'sorted': all in one place.

Of course, the team maintain only a very small amount of the LaTeX 'ecosystem': there are over 5000 packages on [CTAN](https://ctan.org). To help users know whether a bug should be reported to the team or not, we have created the [`latexbug` package](https://github.com/latex3/latexbug).  An example using it:

```latex
\RequirePackage{latexbug}

\documentclass{article}

\begin{document}

Problems here

\end{document}

```

will give a warning if there is any code that isn't covered by the team (and so should be reported elsewhere). We hope this helps bugs get to the right places as easily as possible.

---

I handled most of the conversion from Subversion to Git, and I'd like to acknowledge [SubGit](https://subgit.com/) from TMate Software for making the process (largely) painless. As LaTeX is an open source project, we were able to use this tool for free. We used SubGit for the 'live' mirroring of LaTeX3 to GitHub for several years, and it worked flawlessly. The same was true for the trickier task of moving LaTeX2e: the repo history had a few wrinkles that we slightly more difficult to map to Git, but we got there.
