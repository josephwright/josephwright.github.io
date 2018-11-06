---
title: 'biblatex: A new syntax for \DeclareNameFormat'
layout: post
permalink: /2016/03/13/biblatex-a-new-syntax-for-declarenameformat/
categories:
  - biblatex
  - Packages
---
The 'traditional' BibTeX model for dividing up names is based around four parts:

- First name(s)
- Last name(s)
- Prefix(es) (the 'von part')
- Suffix(es) (the 'junior part')

This works well for many western European names, but falls down for many cases.

As part of Biber/[`biblatex`](http://ctan.org/plg/biblatex) developments, Philippe Kime has been working on moving beyond this rigid model for names to allow true flexibility. However, this comes with a caveat: a [breaking change to `\DeclareNameFormat` in `biblatex`](https://github.com/plk/biblatex/issues/372). The older syntax takes hard-wired arguments for each name part, but that obviously can't be extended. The new format only deals with one argument (the name as a whole), but this requires changes to (non-standard) styles.

At the moment, the change is _only true for Biber_, which means some conditional code is needed. The best way to do that is to test for the older (BibTeX) back-end. For example, in the latest release of [`biblatex-chem`](https://ctan.org/pkg/biblatex-chem) I have in `chem-acs.bbx`:

<!-- {% raw %} -->
```latex
% Modify the name format
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
```
<!-- {% endraw %} -->

I'll deal with the differences in back-ends in another post, but for the present this formulation will keep styles working for everyone.
