---
id: 706
title: From \newcommand to \NewDocumentCommand
date: 2010-05-23T09:54:09+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=706
permalink: /2010/05/23/from-newcommand-to-newdocumentcommand/
categories:
  - LaTeX3
tags:
  - xparse
---
Following on from my [last post](/2010/05/22/promoting-xparse/), I thought it might be useful to give some simple example of how the [`xparse`](https://ctan.org/pkg/xparse) package works and why it's useful. I want to do this to show end users of LaTeX how it can replace `\newcommand`, so the example will not involve anything too complex, code-wise.

First, why would you want to use xparse's `\NewDocumentCommand` in place of `\newcommand`? First, `\NewDocumentCommand` can make macros that take a mixture of arguments that `\newcommand` cannot. With `\newcommand`, you can make a macro that takes a number of mandatory arguments, or ones where the first argument is option and in square brackets, but that is it. Anything else then needs the use of TeX programming or internal LaTeX macros: not really helpful for end users. The second thing is that `\newcommand` macros are not ‘robust’. This shows up where you need to `\protect` things, which can be very confusing. Macros created with `\NewDocumentCommand` are robust, and this means that they work more reliably.

I'm going to illustrate moving from `\newcommand` to `\NewDocumentCommand` with a series of simple examples. For all of them, you need to load the xparse package:

```latex
\usepackage{xparse}
```

## Macros with no arguments

The simplest type of macro is one with no arguments at all. This isn't going to show off xparse very much but is is a starting point. The traditional method to do this is

```latex
\newcommand\NoArgs{Text to insert}
```

which becomes

```latex
\NewDocumentCommand\NoArgs{}{Text to insert}
```

That does not look too bad, I hope. Notice that I've got an empty argument in the xparse case: this is where the arguments are listed, and with `\NewDocumentCommand` there always has to be a list of arguments, even if it is empty. That's a contrast with the `\newcommand` approach, where we only need to mention arguments when there are any.

## One or more mandatory arguments

The most common type of argument for a macro is a mandatory one. With `\newcommand`, we'd give a number of arguments to use:

```latex
\newcommand\OneArg[1]{Text using #1}
\newcommand\TwoArgs[2]{Text using #1 and #2}
```

\NewDocumentCommand is a bit different. Since it can work with different types of argument, each one is give separately as a letter. A mandatory argument is ‘`m`’, so we'd need

```latex
\NewDocumentCommand\OneArg{m}{Text using #1}
\NewDocumentCommand\TwoArgs{mm}{Text using #1 and #2}
```

This is still pretty similar to `\newcommand`: the useful stuff starts when life gets a little more complicated.

## One of more optional (square brackets) arguments

To really get something clever out of xparse, the arguments need to be a little more varied than I've show so far. Let's look at optional arguments, which LaTeX puts in square brackets. If I want the first argument to be optional, then LaTeX can help me

```latex
\newcomand\OneOptOfTwo[2][]{Text with #2 and perhaps #1}
\newcomand\OneOptOfThree[3][]{Text with #2, #3 and perhaps #1}
```

If I want anything else, I'm on my own (so no more `\newcommand` examples!). First, let's do the two example using xparse. An optional argument in square brackets, which works like a `\newcommand` one, is ‘`O`’ followed by `{}`:

```latex
\NewDocumentCommand\OneOptOfTwo{O{}m}%
  {Text with #2 and perhaps #1}
\NewDocumentCommand\OneOptOfTwo{O{}mm}%
{Text with #2, #3 and perhaps #1}
```

How about two optional arguments? It's pretty obvious:

```latex
\NewDocumentCommand\TwoOptOfThree{O{}O{}m}%
  {Text with #3 and perhaps #1 and #2}
```

What if we want something as a default value for the optional argument? With `\newcommand`, that would be

```latex
\newcommand\OneOptWithDefault[2][default]%
  {Text using #1 (could be the default) and #2}
```

which would become

```latex
\NewDocumentCommand\OneOptWithDefault{O{default}m}%
  {Text using #1 (could be the default) and #2}
```

The same idea applies to each optional argument: whatever is in the braces after the `O` is the default value.

## More complex optional arguments

You might be wondering why we need the ‘`{}`c after ‘`O`’ when there is no default value: why not just ‘`o`’? Well, there is ‘`o`’ as well. Unlike `\newcommand`, `\NewDocumentCommand` can tell the difference between an option argument that is not given and one that is empty. To do that, it provides a test to see if the argument is empty:


<!-- {% raw %} -->
```latex
\NewDocumentCommand\OneOptOfTwoWithTest{om}{%
  \IfNoValueTF{#1}
    {Do stuff with #2 only}
    {Do stuff with #1 and #2}%
}
```
<!-- {% endraw %} -->

Don't worry if you forget to do the test: the special marker that is used here will simply print ‘-NoValue-’ as a reminder!

## Two types of optional argument

Sometimes you might want two different optional arguments, and be able to tell which is which. This can be done by using something other than square brackets, often using angle brackets (‘&lt;’ and ‘&gt;’). We can do that using the letter ‘`d`’ (or ‘`D`’ if we give a default).

```latex
\NewDocumentCommand\TwoTypesOfOpt{D&lt;&gt;{}O{}m}%
  {Text using #1, #2 and #3}
```

What input syntax does this make? Let's look at some examples

```latex
\TwoTypesOfOpt{text}             % One mandatory
\TwoTypesOfOpt[text]{text}       % A normal optional
\TwoTypesOfOpt&lt;text&gt;{text}       % A special optional
\TwoTypesOfOpt&lt;text&gt;[text]{text} % Both optionals
```

How did that work? The first two characters after the ‘`D`’ are used to find the optional argument, so in this case ‘`&lt;`’ and ‘`&gt;`’.

## Finding stars or other special markers

Another common idea in LaTeX is to use a star to indicate some special version of a macro. Creating those with `\newcommand` is difficult, but it is easy with `\NewDocumentCommand`


<!-- {% raw %} -->
```latex
\NewDocumentCommand\StarThenArg{sm}{%
  \IfBooleanTF#1
    {Use #2 with a star}
    {Use #2 without a star}%
}
```
<!-- {% endraw %} -->


Here, ‘`s`’ represents a star argument. You'll see that it ends up as `#1`, while the mandatory argument is `#2`. You'll also see that there needs to be a test to see if there is a star (`\IfBooleanTF`). This doesn't mention stars as the test can be used for other things.

## Summing up

There is more to xparse than I've mentioned here, but I hope that this is a useful flavour of what it can be used for. To get more flexibility there is a bit more to think about compared to `\newcommand`, but the overall consistency is hopefully worth it.
