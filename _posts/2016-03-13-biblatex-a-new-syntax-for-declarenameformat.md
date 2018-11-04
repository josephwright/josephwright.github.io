---
id: 1867
title: 'biblatex: A new syntax for \DeclareNameFormat'
date: 2016-03-13T13:20:59+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1867
permalink: /2016/03/13/biblatex-a-new-syntax-for-declarenameformat/
categories:
  - biblatex
  - Packages
---
The 'traditional' BibTeX model for dividing up names is based around four parts:
<ul>
 	<li>First name(s)</li>
 	<li>Last name(s)</li>
 	<li>Prefix(es) (the 'von part')</li>
 	<li>Suffix(es) (the 'junior part')</li>
</ul>
This works well for many western European names, but falls down for many cases.

As part of Biber/<a href="http://ctan.org/plg/biblatex"><code>biblatex</code></a> developments, Philippe Kime has been working on moving beyond this rigid model for names to allow true flexibility. However, this comes with a caveat: a <a href="https://github.com/plk/biblatex/issues/372">breaking change to <code>\DeclareNameFormat</code> in <code>biblatex</code></a>. The older syntax takes hard-wired arguments for each name part, but that obviously can't be extended. The new format only deals with one argument (the name as a whole), but this requires changes to (non-standard) styles.

At the moment, the change is <em>only true for Biber</em>, which means some conditional code is needed. The best way to do that is to test for the older (BibTeX) back-end. For example, in the latest release of <a href="http://ctan.org/pkg/biblatex-chem"><code>biblatex-chem</code></a> I have in <code>chem-acs.bbx</code>:
<pre><code>% Modify the name format
\@ifpackageloaded{biblatex_legacy}
  {
    % Original syntax for BibTeX model
    \DeclareNameFormat{default}{%
      \renewcommand*{\multinamedelim}{\addsemicolon\addspace}%
      \usebibmacro{name:last-first}{#1}{#4}{#5}{#7}%
      \usebibmacro{name:andothers}%
    }

    \DeclareNameFormat{editor}{%
      \renewcommand*{\multinamedelim}{\addcomma\addspace}%
      \usebibmacro{name:last-first}{#1}{#4}{#5}{#7}%
      \usebibmacro{name:andothers}%
    }
  }
  {
   % New syntax for flexible back end
    \DeclareNameFormat{default}{%
      \renewcommand*{\multinamedelim}{\addsemicolon\addspace}%
      \nameparts{#1}%
      \usebibmacro{name:family-given}
        {\namepartfamily}
        {\namepartgiveni}
        {\namepartprefix}
        {\namepartsuffix}%
      \usebibmacro{name:andothers}%
    }

    \DeclareNameFormat{editor}{%
      \renewcommand*{\multinamedelim}{\addcomma\addspace}%
      \nameparts{#1}%
      \usebibmacro{name:family-given}
        {\namepartfamily}
        {\namepartgiveni}
        {\namepartprefix}
        {\namepartsuffix}%
      \usebibmacro{name:andothers}%
    }
  }
</code></pre>
I'll deal with the differences in back-ends in another post, but for the present this formulation will keep styles working for everyone.