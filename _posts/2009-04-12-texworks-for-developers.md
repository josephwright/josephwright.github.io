---
title: TeXworks for developers
layout: post
permalink: /2009/04/12/texworks-for-developers/
categories:
  - TeXworks
---
The [TeXworks](https://tug.org/texworks) program is aim at making using TeX easier for day-to-day TeX users. By stripping the interface down to a minimum, I feel it really succeeds. I'm sure that many experienced TeX developers prefer more “full featured” editors (such as [WinEdt](http://www.winedt.com) on Windows or [AUCTeX](http://www.gnu.org/software/auctex/) on Linux). However, I find that I rarely use any of the more complex features of these richer editors, and so I'm using TeXworks for both day-to-day documents and writing LaTeX packages.

There are still a few things I'd like to have in TeXworks that are currently lacking, but I'm hoping that as the program develops it will be possible to do some user extension and add on what I'd like.  For example, I'd like to be able to use hard line wrapping (with a fixed number of characters in a line) and to delete lines of text rapidly (“killing” them). What I have been able to do so far is create some customised syntax highlighting and some completion code, similar to [DTX submode](http://www.winedt.org/Config/modes/DTX.php) for WinEdt. At the moment, the syntax highlighting I've gone for looks like:

```
[dtx patterns]

# comments
red		Y	\^\^A.*

# special characters
darkred		N	[$#^_{}&amp;]

# Guards
gold		N	%&lt;(?:[A-Za-z0-9!\|]+|.)&gt;
limegreen	N	%&lt;\*(?:[A-Za-z0-9!\|]+|.)&gt;
crimson		N	%&lt;/(?:[A-Za-z0-9!\|]+|.)&gt;

# Macrocode
green		N	^%[\s]{4}\\(?:begin|end)\{macrocode\}

# LaTeX environments
darkgreen	N	\\(?:begin|end)\s*\{[^}]*\}

# LaTeX packages
darkblue	N	\\usepackage\s*(?:\[[^]]*\]\s*)?\{[^}]*\}

# control sequences
blue		N	\\(?:[A-Za-z@:_]+|.)

# Non-code
grey		Y	%.*
```

which is certainly helping me to improve my understanding of regex writing! There are a few things I can't seem to get working quite as I'd ideally like, but for the moment I'm happy.

For auto-completion, I've had to make some assumptions about the beginnings of lines, to get the % characters correct:

```latex
%%!TEX encoding = UTF-8 Unicode
arg:=\Arg{#INS#}
bcode:=    \begin{macrocode}#RET##INS##RET#%    \end{macrocode}#RET#•
benv:=\begin{environment}{#INS#}#RET#%•#RET#%\end{environment}#RET#%•
bmac:=\begin{macro}{#INS#}#RET#%•#RET#%\end{macro}#RET#%•
cc:=\changes{#INS#}{•}{•}#RET#•
cmd:=\cmd{#INS#}
cs:=\cs{#INS#}
denv:=\DescribeEnv{#INS#}
dmac:=\DescribeMacro{#INS#}
dopt:=\DescribeOption{#INS#}
ecode:=    \end{macrocode}#RET##INS#%    \begin{macrocode}#RET#•
eenv:=\end{environment}#RET#
emac:=\end{macro}#RET#
m:=\meta{#INS#}
meta:=\meta{#INS#}
pkg:=\pkg{#INS#}
\Arg{#INS#}
\changes:=\changes{#INS#}{•}{•}#RET#•
\cmd{#INS#}
\cs{#INS#}
\meta{#INS#}
\pkg{#INS#}
```

I'd be interested to hear how other people find TeXworks for writing TeX code, and of course for any contributions to my configuration ideas.
