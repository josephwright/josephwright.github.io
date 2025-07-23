---
title: achemso installation
layout: post
permalink: /2009/11/28/achemso-installation/
categories:
  - achemso
  - Packages
---
One question that crops up from time to time is 'How do I install [`achemso`](https://ctan.org/pkg/achemso)?' For most people, I tend to point out that the latest [MiKTeX](https://www.miktex.org/) and [TeX Live](https://tug.org/texlive/) distributions include both `achemso` and everything it needs to work. So on a stand-alone system, installing an up-to-date distribution is the easiest way.

Manually installing `achemso` itself is not too hard, the main problem being that people miss out the BibTeX files (`achemso.bst` and `biochem.bst`), then get odd effects with bibliographies. On [CTAN](https://www.ctan.org), the file [`achemso`.tds.zip](http://www.ctan.org/cgi-bin/filenameSearch.py?filename=`achemso`.tds.zip&Search=Search) contains everything laid out ready for installation, and that includes the BibTeX files. So my advice for those who can't or don't want to do a full update is to use the TDS `.zip`. For those who want to extract from the source and do everything themselves, as I say the main thing is not to forget the BibTeX styles.

One problem that comes up is the need for a reasonably recent copy of [`xkeyval`](https://ctan.org/pkg/xkeyval). If I was writing the code again from scratch, I probably would not use xkeyval, but that is not the situation. I've worked quite hard to reduce the problems, and the latest version of `achemso` uses only the most basic functions in `xkyeval`. One of the reasons that life is a bit complex is because `xkeyval` requires installation of items in both `tex/generic/xkeyval` and `tex/latex/xkeyval`: not ideal. At the moment, there is no TDS `.zip` on CTAN for `xkeyval`, but I'm always happy to send anyone who needs one a suitable `.zip` by e-mail.
