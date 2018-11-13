---
title: The .dtx format
layout: post
permalink: /2009/10/05/the-dtx-format/
categories:
  - General
tags:
  - DTX
---
A few comments and e-mails have prodded me to put down some thoughts on sorting out LaTeX packages. My original thought was to do one post, but I think a few are needed. So this is the first of a related series: probably three or four posts. I'm going to start with an overview of the DTX format, used for the source of a lot of LaTeX packages.

# Why `.dtx` at all?

The first question to consider is why people bother with the `.dtx` format. Not everyone does, and there are good arguments for and against each different approach. I could easily write an entire post just discussing the various alternatives, but that's not what I want to do here!

The `.dtx` format is favoured by the LaTeX team, and so is something of a standard for LaTeX package authors. The idea of the `.dtx` format is that it allows the package author to put the user documentation, code documentation and code itself in one place.  The user documentation can be typeset on its own, or the user and code documentation can be typeset together (_literate programming_). The code can also be extracted from the source for use: this means that more than one file can be included in the same source. This last point is perhaps the biggest selling point of the `.dtx` format: you can include LaTeX package, class and some configuration files in one source. There is also a speed gain from removing redundant (comment) lines from a package: on a modern PC, this is pretty tiny, but was a bigger point in the past.

# How the format comes about

The `.dtx` format is really defined by two mechanisms, provided by two separate (La)TeX packages. The ability to take one source file and generate several production files, with the comments removed, is provided by the DocStrip package (which is written in plain TeX). Documenting the code, and providing user details, is supported by a dedicated LaTeX class: `ltxdoc`. (This is itself based on the doc class, but I'm going to focus on `ltxdoc`.) The combination of the syntax for the two parts of the mechanism leads to the `.dtx` file format.

It is quite possible to use `.dtx` files as the source for things other than (La)TeX files. Indeed, in my second post I'm going to use the `.dtx` format to also include a plain text file in the source. However, I'm not going to talk about making changes to include other types of code: this is doable, but a bit advanced to go into here!

## DocStrip: guards and extracting

The DocStrip TeX file provides a mechanism to do two related tasks:

1. Remove the comment lines from a source file
2. Produce several production files from one source

To do this, the source file itself (normally a `.dtx` file) needs to be accompanied by a set of instructions on how to do the extraction (normally a `.ins` file). The two tasks are inter-related: DocStrip always has to generate a new file to remove the comment lines, even if the source is only for one file.

Removing the comment lines is relatively easy to understand. Any line in the source starting with one `%` will not appear in the generated file(s). So code lines in the source are written as normal, and any comments that should appear in the generated files need to start with two (or more) `%` characters.

The more complex idea is setting up the source so that several files can be generated from one source. This uses so-called guards to indicate what goes with what. Let's imagine we have a very simple source, which will be used to generate two LaTeX packages. The two packages share some code, so we don't want to repeat it in the source file.

```latex
%&lt;*PackageA&gt;
Code just for package A
%&lt;/PackageA&gt;
%&lt;*PackageB&gt;
Code just for package B
%&lt;/PackageB&gt;
%&lt;*PackageA|PackageB&gt;
Code for both packages
%&lt;/PackageA|PackageB&gt;
```

What is happening here? Each guard line is a comment (so it will not appear in the production file), and is enclosed in angle brackets. The first line, `%&lt;*PackageA&gt;`, is a guard starting lines that will only appear when extracting `PackageA`. That continues until the matching closing guard, `%&lt;/PackageA&gt;`. There is then a section that applies only to `PackageB`, marked up in much the same way. The final set of guards use the `|` symbol to mean 'or': lines here will appear in both `PackageA` and `PackageB`. You can do more complex things (nest guards, use `&amp;` as a logical 'and', _etc_.), but the basic idea remains the same.

I've said a couple of times that the code is extracted, and that this needs some instructions for DocStrip. Essentially, this means matching up the names of the guards with the files they relate to. In my simple example, a suitable DocStrip `.ins` file would be

```latex
\input docstrip
\askforoverwritefalse
\generate{
  \file{PackageA.sty}{\from{example.dtx}{PackageA}}
  \file{PackageB.sty}{\from{example.dtx}{PackageB}}
}
```

Here, I've assumed the `.dtx` file is called `example.dtx`. I'm only using one `.dtx` file, and one guard for each output file. As with many other parts of DocStrip, there is more you can do.

Multiple guards can be used for each package, so if we had lots of packages with some common code, we might well have:

```latex
\input docstrip
\askforoverwritefalse
\generate{
  \file{PackageA.sty}{\from{example.dtx}{PackageA,common}}
  \file{PackageB.sty}{\from{example.dtx}{PackageB,common}}
  \file{PackageC.sty}{\from{example.dtx}{PackageC,common}}
}
```

and so on.

So DocStrip lets us extract code out, have common sections, remove comments and so on. However, it doesn't help with the documentation side at all: that is all just comments to DocStrip.

## `ltxdoc`: documenting the source

The `ltxdoc` class is the typesetting part of the `.dtx` format. The idea is that the `.dtx` is read in by a driver file, which actually does the typesetting. When the `.dtx` is read in this way, the comment characters are ignored, meaning that what DocStrip sees as comments are the source for typesetting the `.dtx`. In practice, most `.dtx` files are written so that the driver is part of the `.dtx` itself. The driver part of a `.dtx` is normally very simple

```latex
\documentclass{ltxdoc}
% Perhaps some \usepackage instructions
\begin{document}
  \DocInput{\jobname.dtx}
\end{document}
```

Usually, the documentation and code then follows after `\end{document}`: with some correctly placed `%\iffalse` ... `%\fi` constructions, the driver part is then skipped and the documentation and code is typeset.

In the documentation part, the usual LaTeX mark-up can be used, with a few additional macros.

- `\cs{_&lt;name&gt;_}` is used to print a function name, including the leading backslash, in a fixed-width font (and avoiding any category-code issues with the backslash).
- `\meta{_&lt;argument&gt;_}` prints the name of an argument surrounded by angle brackets and printed in italic, so it stands out (as I've tried to do here using HTML!).
- \marg{_&lt;argument&gt;_} and `\oarg{_&lt;argument&gt;_}` print mandatory and optional arguments as '{_&lt;argument&gt;_}' and '[_&lt;argument&gt;_]', respectively.
- `\DescribeMacro _&lt;csname&gt;_` prints the argument name as a marginal note, and includes it for indexing and cross-referencing.

In the code section, the code itself is marked off from the documentation both by comment characters (for DocStrip), and some macros for `ltxdoc`:

```latex
%\begin{macro}{\MyMacro}
% This is some text which should explain the code.
%    \begin{macrocode}
\newcommand*\MyMacro[1]{Code here!}
%    \end{macrocode}
%\end{macro}
```

The `\begin{macro}` ...`\end{macro}` block is used so that cross-references between the code and index work correctly. They are used to show that this block defines `\MyMacro` (rather than just using it). On the other hand, `\begin{macrocode}` ... `\end{macrocode}` tells `ltxdoc` where the code is, so that it prints correctly. For mainly historical reasons, there have to be exactly four spaces in `%    \end{macrocode}`!

There are, again, several extra ideas that can be used in the code parts of `ltxdoc`. However, to try to explain all of them would be to make this post completely impossible to read!

# Putting everything together

There is a lot to take in in the `.dtx` format, and a quick survey of [CTAN](https://www.ctan.org) will show that there are lots of ways of using it (before you even look at other approaches). In the next post on this subject, I'm going to present the approach I've developed to producing `.dtx` files (with a lot of ideas taken from others, in particular Will Robertson). The aim is to have a single source for the README, `.ins` file, documentation and LaTeX code. We'll see how it's possible to do that, and to have the code extract by running `tex my.dtx` and to typeset the package using `latex my.dtx`.
