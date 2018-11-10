---
title: 'Programming LaTeX3: Creating functions'
layout: post
permalink: /2011/12/14/programming-latex3-creating-functions/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
Teaching a programming language traditionally starts with a method to print 'Hello World'. For programming LaTeX3, we can't quite start there as

```latex
\documentclass{article}
\begin{document}
Hello world
\end{document}
```

will happily do that without needing any programming. So I'll start by printing 'Hello World' _lots_ of times!

## Our first function

LaTeX3 has a built-in method for creating multiple copies of text, which we could use directly. However, that would mean using a code-level macro in the document itself, and so I'll create a wrapper macro. For this first example, I'll include all of the document:

```latex
\documentclass{article}
\usepackage{expl3}
\ExplSyntaxOn
\cs_new:Npn \SayHello #1
  { \prg_replicate:nn {#1} { Hello~World!~ } }
\ExplSyntaxOff
\begin{document}
\SayHello{100}
\end{document}
```

This will give you, as promised, 100 copies of 'Hello World!'.

So what is going on here? As you might work out, I've defined a new command called `\SayHello` which prints as many copies of 'Hello World!' as requested. Later on we'll see that this is usually not how I'd choose to create a 'document command', but for the moment I'll pass over that point so we can get some basics established.

## The structure of function names

Getting down to detail, I've introduced two LaTeX3 functions here: `\cs_new:Npn` and `\prg_replicate:nn`. [As promised](/2011/12/11/programming-latex3-the-programming-environment/), these use `:` and `_` as 'letters' in their names. But what do they do? As you might guess from the names, `\cs_new:Npn` is used to create a new control sequence, while `\prg_replicate:nn` makes lots of copies of something (it replicates stuff). The naming convention for LaTeX3 is that the first part of the name (`\cs_...` or `\prg_...`) refers to the _module_ the function comes from. So `\cs_new:Npn` is from the module for control sequences, which we abbreviate as `cs`, while `\prg_replicate:nn` is from the general programming utilities module, which is abbreviated as `prg`. For programmers working outside of the LaTeX3 kernel, a module is probably going to be the same as a LaTeX2e package. So the module part of the name is used to divide up code into related blocks: each module should use a unique prefix, and I'll tend to use `\mypkg...` for demonstration purposes.

Up to the `:`, the rest of the name is up to the programmer and should help you understand what a function does. So `\cs_new:Npn` tells us that the function makes new a control sequence, and so is pretty similar to LaTeX2e's `\newcommand`. We can have multiple parts to the name divided by `_` for ease of reading. For example `\cs_new_nopar:Npn` is available for creating new functions which will give an error if they pick up a `\par`: this is similar to `\newcommand*`. You can probably work out the analysis of `\prg_replicate:nn` yourself!

The part of the name after the `:` is perhaps one of the most confusing ideas for new LaTeX3 programmer, especially if they are used to other languages. It's called the _argument specification_ or _signature_ of the function, and tells us about the number and type of arguments a function takes. If you have experience in other programming languages, you're probably wondering why we include this information in the function name. As we'll see as we look in more detail at LaTeX3, this approach works as it reflects how TeX works.

So what do the different letters mean? Each letter (usually) represents one argument for a function. So `\prg_replicate:nn` with two letters after the `:` needs two arguments. (For those of you who haven't come across arguments before, something like `\maketitle` takes no arguments, `\emph` needs one argument, `\setlength` takes two arguments, and so on.) The letter itself then tells us about the type of argument: `n` means tokens in braces (a 'normal' argument).  In `\cs_new:Npn`, the `n`-type argument is the code which we are creating. An `N` means that the argument has to be a single token _without_ any braces: in our current case this will be the name of the new function. The `p` is a bit more complicated: it means that the second argument here is a parameter specification. Here, we can use `#1`, `#2`, _etc._, to represent the arguments for the new function, in exactly the same way we do in the code. So when we use `\SayHello`, it will expect to find one argument, and will insert that into the place marked as `#1` in the code part.

## Analysis `\prg_replicate:nn`

The same analysis applies to `\prg_replicate:nn`, which we can now see needs two arguments, both in braces. The first one is the number of times to repeat, and the second argument is what to repeat. So in `\SayHello` the number of repetitions is supplied by the user (this will replace `#1`), but the text is fixed by the programmer.

The reference for finding out what functions are available, and what arguments they take, is [interface3](http://mirror.ctan.org/macros/latex/contrib/l3kernel/interface3.pdf). I'll only be covering a selection of what is available, so over time you'll need to get familiar with the formal documentation to find out what you can do. If you take a look there, you'll see that the first argument for `\prg_replicate:nn` is an _integer expression_. That means that we don't have to use a number directly here, but can also use something that will result in a number once TeX has worked it out. That will carry through to our user function, so

```latex
\SayHello{ 10 - 3 + 4 }
```

will be valid input.

## Functions or macros?

Experienced TeX programmers will probably be worried that I'm talking about 'functions' and not about 'macros'. TeX is a macro expansion language, which means that when it reads `\SayHello`, it replaces it by the code we've defined as the meaning of `\SayHello`, then reads the start of the inserted code, replaces it as necessary and so on until it has something to typeset (such as a letter) or execute (a 'primitive'). That means that programming TeX is very different from programming using true functions.

The LaTeX3 programming approach allows us to treat many macros as if they were functions, but there are places where we'll need to think about macros being expanded. Throughout the LaTeX3 documentation, programming is described in terms of functions, and so I'll stick to that approach. Bear in mind that underlying everything is a set of macros, and that this will show up from time to time.
