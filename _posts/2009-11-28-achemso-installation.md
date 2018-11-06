---
id: 572
title: achemso installation
date: 2009-11-28T18:53:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=572
permalink: /2009/11/28/achemso-installation/
categories:
  - achemso
  - Packages
---
One question that crops up from time to time is “How do I install <a title="Support for American Chemical Society journal submissions" href="http://ctan.org/pkg/achemso">achemso</a>?” For most people, I tend to point out that the latest <a title="MiKTeX Homepage" href="http://www.miktex.org/">MiKTeX</a> and <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> distributions include both achemso and everything it needs to work. So on a stand-alone system, installing an up-to-date distribution is the easiest way.

Manually installing achemso itself is not too hard, the main problem being that people miss out the BibTeX files (achemso.bst and biochem.bst), then get odd effects with bibliographies. On <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a>, the file <a href="http://www.ctan.org/cgi-bin/filenameSearch.py?filename=achemso.tds.zip&amp;Search=Search">achemso.tds.zip</a> contains everything laid out ready for installation, and that includes the BibTeX files. So my advice for those who can't or don't want to do a full update is to use the TDS zip. For those who want to extract from the source and do everything themselves, as I say the main thing is not to forget the BibTeX styles.

One problem that comes up is the need for a reasonably recent copy of <a href="http://ctan.org/pkg/xkeyval">xkeyval</a>. If I was writing the code again from scratch, I probably would not use xkeyval, but that is not the situation. I've worked quite hard to reduce the problems, and the latest version of achemso uses only the most basic functions in xkyeval. One of the reasons that life is a bit complex is because xkeyval requires installation of items in both <code>tex/generic/xkeyval</code> and <code>tex/latex/xkeyval</code>: not ideal. At the moment, there is no TDS zip on CTAN for xkeyval, but I'm always happy to send anyone who needs one a suitable zip by e-mail.
