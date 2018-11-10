---
title: File operation limitations
layout: post
permalink: /2010/12/31/file-operation-limitations/
categories:
  - General
tags:
  - newread
  - newwrite
  - registers
---
In my [previous post](/2010/12/30/local-register-allocation/), I looked at the concept of register allocation in TeX. What I did not talk about there was how many registers are available, as this is a little more complex. When Knuth wrote TeX, he gave 256 register of each type for storing data. So you can use `\count0` to `\count255`, `\toks0` to `\toks255`, _etc._ Some of these are 'special', so the number available for general use is slightly less, but the general concept is clear. Subsequent engines have extended the number of these registers a lot: the e-TeX extensions give us 32768 registers of each type! Using these requires a modified allocation system, which for LaTeX is provided by the `etex` package.

You'll notice I've not mentioned file reading and writing in the above. There is a reason for this: they are different. TeX provides only 16 read and write streams, and this limit is retained in later engines. There is a reason for this: having lots of files open is not generally regarded as a good idea.

Having only 16 file streams available is clearly a bit limiting, particularly because the TeX `\newwrite` allocation never frees anything back up. Once a file stream has been used for one file it is never available for anything else. Many LaTeX users will be familiar with the potential result of this

```latex
No room for a new \write
```

(The limitation on reading files does not show up so often in real cases, but is also there.)

I've had a couple or requests recently asking what can be done about this. First, a bit more background. When TeX opens a file for writing, it wipes out any previous content. So you cannot keep opening and closing a file you need to add to: once it's open, you don't want to close it until you are done. This sounds awkward, but there are alternative approaches.

In [LaTeX3](https://www.latex-project.org/latex3.html), what we've implemented is a pool system. The idea is that rather than permanently allocating a stream, the programmer only uses one while it is needed, and then closes it. We've also strongly suggested that most file operations can happen in 'one shot', with all of the information saved in TeX's memory until the end of the document. This can be done for anything which is written using `\immediate\write`, but for stuff written at `\shipout` then the file does have to be open. I'm hoping that most file writing operations fall into the first category! The biggest problem with this change is that it will only work with rewritten code, which does not help with existing packages now.

An alternative approach is implemented by the [`rvwrite`](https://ctan.org/pkg/rvwrite) package. It uses a single file, which is marked up in different parts for different uses. After the LaTeX run, this special file is then reprocessed to split out all of the separate parts. So there is no limit on how many files can be created. However, existing code still needs to be rewritten to use this new mechanism, and of course the user has to do an extra step.

One obvious question is 'what about [LuaTeX](http://www.luatex.org/)?'. It keeps the 16 file limit at the TeX end, but Lua has no hard limit and so can easily get around this. However, the same issue of needing to rewrite code applies as with any other solution.

So it seems we are stuck with a 16 file limit for a while yet. All of the improved approaches need new code to be written, as simply changing the way `\newwrite` works will simply break existing packages. However, there are better alternatives, and if people know about them then hopefully things will improve.
