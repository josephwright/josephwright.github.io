---
title: Finding files by expansion
layout: post
permalink: /2019/09/06/finding-files-by-expansion
categories:
  - LaTeX3
---

## The TeX core situation

Loading files is an important part of using TeX. At the primitive level,
reading an entire file is done using `\input`. As many people know, files are
found by a TeX system using the `kpathsea` library, which means that the
argument to `\input` should (usually) be the file name alone.

However, it's often convenient to have files found in subdirectories of a
project: the LaTeX2e `\graphicspath` command is perhaps the classic example
where this is used. Looking in multiple places means having an approach to
searching for files. The same idea comes up again with graphics whenever you
use `\includegraphics`: most of the time, you don't give the file extension but
rather let (La)TeX do some searching.

At the same time as this need to search for existing files, there's the issue
of when a file might be missing. The `\input` primitive is pretty unforgiving
if the file is not found, and there are lots of times we want to 'use this file
only' if it actually exists, or to retain control of the error state if
a file is missing.

Classical TeX offers one way to check for files before trying to input them.
That's done by using the `\openin` primitive to open the file, then using an
`\ifeof` test to see if we have reached the end of the file. That works because
a non-existent file gives an immediate end-of-file for a read (`\openin`), but
does not lead to an errors (in contrast to `\input`). The downside to this
approach is it performs an assignment, so is not usable in an expansion context.

Some years ago, pdfTeX introduced a number of 'file information' primitives,
including `\pdffilesize`. This takes a file name, and expands to the size of
the file. Importantly, it works without error with a non-existent file, and
expands to nothing at all. That means that it can be used to know if a file
exists: any value at all means that it does. As the primitive works by
expansion, it also can be used anywhere in TeX.

## Searching in `expl3`

For TeX Live 2019, the LaTeX team [did some
work](/2018/12/06/bringing-xetex-into-line) to bring primitives into line
between XeTeX and other engines. That means that we can now look to exploit
`\pdffilesize` as a way to find files and add new functionality. (The team
  looking after pTeX and upTeX had already added `\pdffilesize`.)

I've just sent an update of [`expl3`](https://ctan.org/pkg/l3kernel) to
[CTAN](https://ww.ctan.org) which uses this new approach to file finding.
There's more to it than just changing the file opening primitive. To do a
search for different paths, we need to be able to check one at a time. The
older `expl3` code checks each possible path using an assignment: again, not
allowed in an expansion context. So I've re-written all of the search code to
work by expansion: tricky but workable.

This means we have some new goodies: things like `\file_size:n` which can
be used inside an `x`-type expansion (`\edef`) to give the size of a file
even if it is not on the standard search path. Of course, being `expl3`
code, everything still handles spaces-in-filenames and active characters
correctly.

## Future plans

At present, where `\pdffilesize` is not available we will still fall back on
the older code, so not everything can be done by expansion. However, in the
near(ish) future we will likely make `\pdffilesize` a required primitive for
`expl3`. At that point, some other code can be made expandable, most
obviously `\file_if_exist:n(TF)`. That will lead to some changes in the minimal
engine versions: more news as and when a change happens.
