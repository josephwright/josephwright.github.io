---
title: Working with .dtx files
layout: post
permalink: /2009/10/11/working-with-dtx-files/
categories:
  - General
tags:
  - DTX
---
I've talked a bit about the [`.dtx` file format](/2009/10/05/the-dtx-format/) and given [an example of a skeleton `.dtx` file](/2009/10/06/a-model-dtx-file/). I thought I'd talk next about working with sources, which will be a bit of a scattered post but will hopefully be interesting!

# Editing `.dtx` files

As with any TeX source, you don't have to have a special editor to work with `.dtx` files, but it can be helpful. Many people say that [Emacs](http://www.gnu.org/software/emacs/) (using [AUC-TeX](http://www.gnu.org/software/auctex/)) has the best `.dtx` editing mode of all: I've only tried it briefly, but the AUC-TeX homepage has the details. On Windows, [WinEdt](http://www.winedt.com/) has a pretty strong `.dtx` Submode which does similar things. As I mainly use [TeXworks](https://tug.org/texworks), I've made a few modifications to get something similar to those two 'leaders': at the moment I use the following settings for syntax highlighting:

```
[LaTeX DTX]

# comments
red        Y    \^\^A.*

# Guards
orange        N    %&lt;(?:[A-Za-z0-9!\|]+|.)&gt;
limegreen    N    %&lt;\*(?:[A-Za-z0-9!\|]+|.)&gt;
crimson        N    %&lt;/(?:[A-Za-z0-9!\|]+|.)&gt;

# special characters
darkred        N    \^\^\^\^\^[0-9a-z]{5}
darkred        N    \^\^\^\^[0-9a-z]{4}
darkred        N    \^\^\^[0-9a-z]{3}
darkred        N    \^\^[0-9a-z]{2}
darkred        N    [$#^_{}&amp;]
gray        N    ^%%.*
gray        N    ^%

# Macrocode
green        N    \\(?:begin|end)\{macrocode\}

# LaTeX environments
darkgreen    N    \\(?:begin|end)\s*\{[^}]*\}

# control sequences
blue        N    \\(?:[A-Za-z@:_]+|.)
```

plus a few special auto-complete entries. Not quite up with the best just yet, but it's still early days for TeXworks.

# What to document

Getting documentation right is not easy. My general approach is to try to include lots of examples, so I always load the package being talked about for the documentation. That means I can use the package 'in place'. Unfortunately, `ltxdoc` does not have a built-in example environment. I use the [`listings`](https://ctan.org/pkg/listings) package, and although it's a bit complex looking, the following code works well:

```latex
%\lst@RequireAspects{writefile}
%\newsavebox{\LaTeXdemo@box}
%\lstnewenvironment{LaTeXdemo}[1][code and example]{^^A
%  \global\let\lst@intname\@empty
%  \expandafter\let\expandafter\LaTeXdemo@end
%    \csname LaTeXdemo@#1@end\endcsname
%  \@nameuse{LaTeXdemo@#1}^^A
%}{^^A
%  \LaTeXdemo@end
%}
%\newcommand*\LaTeXdemo@new[3]{^^A
%  \expandafter\newcommand\expandafter*\expandafter
%    {\csname LaTeXdemo@#1\endcsname}{#2}^^A
%  \expandafter\newcommand\expandafter*\expandafter
%    {\csname LaTeXdemo@#1@end\endcsname}{#3}^^A
%}
%\newcommand*\LaTeXdemo@common{^^A
%  \setkeys{lst}{
%    basicstyle   = \small\ttfamily,
%    basewidth    = 0.51em,
%    gobble       = 3,
%    keywordstyle = \color{blue},
%    language     = [LaTeX]{TeX},
%    moretexcs    = {
%      examplemacro,
%      ^^A Add you command names here!
%    }
%  }^^A
%}
%\newcommand*\LaTeXdemo@input{^^A
%  \MakePercentComment
%  \catcode`\^^M=10\relax
%  \small
%  \begingroup
%    \setkeys{lst}{
%      SelectCharTable=\lst@ReplaceInput{\^\^I}{\lst@ProcessTabulator}
%    }^^A
%    \leavevmode
%      \input{\jobname.tmp}^^A
%  \endgroup
%  \MakePercentIgnore
%}
%\LaTeXdemo@new{code and example}{^^A
%  \setbox\LaTeXdemo@box=\hbox\bgroup
%    \lst@BeginAlsoWriteFile{\jobname.tmp}^^A
%    \LaTeXdemo@common
%}{^^A
%    \lst@EndWriteFile
%  \egroup
%  \begin{center}
%    \ifdim\wd\LaTeXdemo@box&gt;0.48\linewidth\relax
%      \hbox to\linewidth{\box\LaTeXdemo@box\hss}^^A
%        \begin{minipage}{\linewidth}
%          \LaTeXdemo@input
%        \end{minipage}
%    \else
%      \begin{minipage}{0.48\linewidth}
%        \LaTeXdemo@input
%      \end{minipage}
%      \hfill
%      \begin{minipage}{0.48\linewidth}
%        \hbox to\linewidth{\box\LaTeXdemo@box\hss}^^A
%      \end{minipage}
%    \fi
%  \end{center}
%}
%\LaTeXdemo@new{code only}{^^A
%  \LaTeXdemo@common
%}{^^A
%}
```

This gets pasted in at the start of the document (after the driver): not great coding style, but not too bad for this job. The idea is that I can then write something like:

```latex
%\begin{LaTeXdemo}
%  Some clever demo here
%\end{LaTeXdemo}
```

and the demonstration will be both typeset as code and actually used. So the user can see the input and the result of whatever I've designed.
Of course, if you are writing LaTeX classes or the like, then this won't work. For my [`achemso` ](https://ctan.org/pkg/achemso)class, I include a demo document in the `.dtx`. This then gets extracted as a separate file (`achemso-demo.tex`), which includes lots of hints in the text and demonstrates as much as possible about the class. Again, the idea is to show how things are done by example: much better than trying to explain in the abstract.

# Releasing stuff to CTAN

In my next post, I'm hoping to talk about automating the process of getting stuff ready for [CTAN](https://www.ctan.org). So here I'll just mention a few general ideas. One is that users shouldn't need to read the code to use a LaTeX package (unless of course you are aiming at supporting other package authors). So I tend to typeset only the user part of the documentation. Normally, it's a good idea to also include an index and list of changes in the pdf documentation, so a typical 'recipe' would be

```bash
pdflatex -draftmode "\AtBeginDocument{\OnlyDescription} \input demopkg.dtx"
makeindex -s gglo.ist -o demopkg.gls demopkg.glo
makeindex --s gind.ist -o demopkg.ind demopkg.idx
pdflatex "\AtBeginDocument{\OnlyDescription} \input demopkg.dtx"
pdflatex "\AtBeginDocument{\OnlyDescription} \input demopkg.dtx"
```

The idea of all this is to only typeset what is needed (hence the `-draftmode` in the first line), to miss out the code (`\OnlyDescription`), and to index both the changes and the user functions (the two `makeindex` lines). This recipe will turn up in the next post as the basis for doing things without needing to remember everything yourself!

CTAN like to have a `.zip` file containing the source, documentation and `.ins` file. They also prefer Unix line endings, so those of us working on Windows have to use something like [Info-ZIP](http://www.info-zip.org/) or the [Swiss File Knife](http://stahlforce.com/dev/index.php?tool=sfk) to alter the line endings. The idea of a TDS-ready `.zip` is also popular, so there are normally two files to get ready. All of that is a bit awkward, especially if like me you keep having to do bug fix releases. So I always do this using an automated tool. I'll talk about this in the next post.
