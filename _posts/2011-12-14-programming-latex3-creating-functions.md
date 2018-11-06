---
id: 1216
title: 'Programming LaTeX3: Creating functions'
date: 2011-12-14T21:38:15+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1216
permalink: /2011/12/14/programming-latex3-creating-functions/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
Teaching a programming language traditionally starts with a method to print ‘Hello World’. For programming LaTeX3, we can't quite start there as
<pre>\documentclass{article}
\begin{document}
Hello world
\end{document}</pre>
will happily do that without needing any programming. So I'll start by printing ‘Hello World’ <em>lots</em> of times!
<h2>Our first function</h2>
LaTeX3 has a built-in method for creating multiple copies of text, which we could use directly. However, that would mean using a code-level macro in the document itself, and so I'll create a wrapper macro. For this first example, I'll include all of the document:
<pre>\documentclass{article}
\usepackage{expl3}
\ExplSyntaxOn
\cs_new:Npn \SayHello #1
  { \prg_replicate:nn {#1} { Hello~World!~ } }
\ExplSyntaxOff
\begin{document}
\SayHello{100}
\end{document}</pre>
This will give you, as promised, 100 copies of ‘Hello World!’.

So what is going on here? As you might work out, I've defined a new command called <code>\SayHello</code> which prints as many copies of ‘Hello World!’ as requested. Later on we'll see that this is usually not how I'd choose to create a ‘document command’, but for the moment I'll pass over that point so we can get some basics established.
<h2>The structure of function names</h2>
Getting down to detail, I've introduced two LaTeX3 functions here: <code>\cs_new:Npn</code> and <code>\prg_replicate:nn</code>. <a title="Programming LaTeX3: The programming environment" href="http://www.texdev.net/2011/12/11/programming-latex3-the-programming-environment/">As promised</a>, these use <code>:</code> and <code>_</code> as ‘letters’ in their names. But what do they do? As you might guess from the names, <code>\cs_new:Npn</code> is used to create a new control sequence, while <code>\prg_replicate:nn</code> makes lots of copies of something (it replicates stuff). The naming convention for LaTeX3 is that the first part of the name (<code>\cs_…</code> or <code>\prg_…</code>) refers to the <em>module</em> the function comes from. So <code>\cs_new:Npn</code> is from the module for control sequences, which we abbreviate as <code>cs</code>, while <code>\prg_replicate:nn</code> is from the general programming utilities module, which is abbreviated as <code>prg</code>. For programmers working outside of the LaTeX3 kernel, a module is probably going to be the same as a LaTeX2e package. So the module part of the name is used to divide up code into related blocks: each module should use a unique prefix, and I'll tend to use <code>\mypkg…</code> for demonstration purposes.

Up to the <code>:</code>, the rest of the name is up to the programmer and should help you understand what a function does. So <code>\cs_new:Npn</code> tells us that the function makes new a control sequence, and so is pretty similar to LaTeX2e's <code>\newcommand</code>. We can have multiple parts to the name divided by <code>_</code> for ease of reading. For example <code>\cs_new_nopar:Npn</code> is available for creating new functions which will give an error if they pick up a <code>\par</code>: this is similar to <code>\newcommand*</code>. You can probably work out the analysis of <code>\prg_replicate:nn</code> yourself!

The part of the name after the <code>:</code> is perhaps one of the most confusing ideas for new LaTeX3 programmer, especially if they are used to other languages. It's called the <em>argument specification</em> or <em>signature</em> of the function, and tells us about the number and type of arguments a function takes. If you have experience in other programming languages, you're probably wondering why we include this information in the function name. As we'll see as we look in more detail at LaTeX3, this approach works as it reflects how TeX works.

So what do the different letters mean? Each letter (usually) represents one argument for a function. So <code>\prg_replicate:nn</code> with two letters after the <code>:</code> needs two arguments. (For those of you who haven't come across arguments before, something like <code>\maketitle</code> takes no arguments, <code>\emph</code> needs one argument, <code>\setlength</code> takes two arguments, and so on.) The letter itself then tells us about the type of argument: <code>n</code> means tokens in braces (a ‘normal’ argument).  In <code>\cs_new:Npn</code>, the <code>n</code>-type argument is the code which we are creating. An <code>N</code> means that the argument has to be a single token <em>without</em> any braces: in our current case this will be the name of the new function. The <code>p</code> is a bit more complicated: it means that the second argument here is a parameter specification. Here, we can use <code>#1</code>, <code>#2</code>, <em>etc.</em>, to represent the arguments for the new function, in exactly the same way we do in the code. So when we use <code>\SayHello</code>, it will expect to find one argument, and will insert that into the place marked as <code>#1</code> in the code part.
<h2>Analysis <code>\prg_replicate:nn</code></h2>
The same analysis applies to <code>\prg_replicate:nn</code>, which we can now see needs two arguments, both in braces. The first one is the number of times to repeat, and the second argument is what to repeat. So in <code>\SayHello</code> the number of repetitions is supplied by the user (this will replace <code>#1</code>), but the text is fixed by the programmer.

The reference for finding out what functions are available, and what arguments they take, is <a href="http://mirror.ctan.org/macros/latex/contrib/l3kernel/interface3.pdf">interface3</a>. I'll only be covering a selection of what is available, so over time you'll need to get familiar with the formal documentation to find out what you can do. If you take a look there, you'll see that the first argument for <code>\prg_replicate:nn</code> is an <em>integer expression</em>. That means that we don't have to use a number directly here, but can also use something that will result in a number once TeX has worked it out. That will carry through to our user function, so
<pre>\SayHello{ 10 - 3 + 4 }
</pre>
will be valid input.
<h2>Functions or macros?</h2>
Experienced TeX programmers will probably be worried that I'm talking about ‘functions’ and not about ‘macros’. TeX is a macro expansion language, which means that when it reads <code>\SayHello</code>, it replaces it by the code we've defined as the meaning of <code>\SayHello</code>, then reads the start of the inserted code, replaces it as necessary and so on until it has something to typeset (such as a letter) or execute (a ‘primitive’). That means that programming TeX is very different from programming using true functions.

The LaTeX3 programming approach allows us to treat many macros as if they were functions, but there are places where we'll need to think about macros being expanded. Throughout the LaTeX3 documentation, programming is described in terms of functions, and so I'll stick to that approach. Bear in mind that underlying everything is a set of macros, and that this will show up from time to time.
