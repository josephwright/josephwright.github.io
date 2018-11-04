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
Following on from my <a href="http://www.texdev.net/2010/05/22/promoting-xparse/">last post</a>, I thought it might be useful to give some simple example of how the <a title="Generic document command parser" href="http://ctan.org/pkg/xparse">xparse</a> package works and why it's useful. I want to do this to show end users of LaTeX how it can replace <code>\newcommand</code>, so the example will not involve anything too complex, code-wise.

First, why would you want to use xparse's <code>\NewDocumentCommand</code> in place of <code>\newcommand</code>? First, <code>\NewDocumentCommand</code> can make macros that take a mixture of arguments that <code>\newcommand</code> cannot. With <code>\newcommand</code>, you can make a macro that takes a number of mandatory arguments, or ones where the first argument is option and in square brackets, but that is it. Anything else then needs the use of TeX programming or internal LaTeX macros: not really helpful for end users. The second thing is that <code>\newcommand</code> macros are not ‘robust’. This shows up where you need to <code>\protect</code> things, which can be very confusing. Macros created with <code>\NewDocumentCommand</code> are robust, and this means that they work more reliably.

I'm going to illustrate moving from <code>\newcommand</code> to <code>\NewDocumentCommand</code> with a series of simple examples. For all of them, you need to load the xparse package:

<pre>\usepackage{xparse}
</pre>

<h2>Macros with no arguments</h2>

The simplest type of macro is one with no arguments at all. This isn't going to show off xparse very much but is is a starting point. The traditional method to do this is

<pre>\newcommand\NoArgs{Text to insert}</pre>

which becomes

<pre>\NewDocumentCommand\NoArgs{}{Text to insert}
</pre>

That does not look too bad, I hope. Notice that I've got an empty argument in the xparse case: this is where the arguments are listed, and with <code>\NewDocumentCommand</code> there always has to be a list of arguments, even if it is empty. That's a contrast with the <code>\newcommand</code> approach, where we only need to mention arguments when there are any.

<h2>One or more mandatory arguments</h2>

The most common type of argument for a macro is a mandatory one. With <code>\newcommand</code>, we'd give a number of arguments to use:

<pre>\newcommand\OneArg[1]{Text using #1}
\newcommand\TwoArgs[2]{Text using #1 and #2}
</pre>

\NewDocumentCommand is a bit different. Since it can work with different types of argument, each one is give separately as a letter. A mandatory argument is ‘<code>m</code>’, so we'd need

<pre>\NewDocumentCommand\OneArg{m}{Text using #1}
\NewDocumentCommand\TwoArgs{mm}{Text using #1 and #2}
</pre>

This is still pretty similar to <code>\newcommand</code>: the useful stuff starts when life gets a little more complicated.

<h2>One of more optional (square brackets) arguments</h2>

To really get something clever out of xparse, the arguments need to be a little more varied than I've show so far. Let's look at optional arguments, which LaTeX puts in square brackets. If I want the first argument to be optional, then LaTeX can help me

<pre>\newcomand\OneOptOfTwo[2][]{Text with #2 and perhaps #1}
\newcomand\OneOptOfThree[3][]{Text with #2, #3 and perhaps #1}
</pre>

If I want anything else, I'm on my own (so no more <code>\newcommand</code> examples!). First, let's do the two example using xparse. An optional argument in square brackets, which works like a <code>\newcommand</code> one, is ‘<code>O</code>’ followed by <code>{}</code>:

<pre>\NewDocumentCommand\OneOptOfTwo{O{}m}%
  {Text with #2 and perhaps #1}
\NewDocumentCommand\OneOptOfTwo{O{}mm}%
{Text with #2, #3 and perhaps #1}</pre>

How about two optional arguments? It's pretty obvious:

<pre>\NewDocumentCommand\TwoOptOfThree{O{}O{}m}%
  {Text with #3 and perhaps #1 and #2}
</pre>

What if we want something as a default value for the optional argument? With <code>\newcommand</code>, that would be

<pre>\newcommand\OneOptWithDefault[2][default]%
  {Text using #1 (could be the default) and #2}
</pre>

which would become

<pre>\NewDocumentCommand\OneOptWithDefault{O{default}m}%
  {Text using #1 (could be the default) and #2}
</pre>

The same idea applies to each optional argument: whatever is in the braces after the <code>O</code> is the default value.

<h2>More complex optional arguments</h2>

You might be wondering why we need the ‘<code>{}</code>c after ‘<code>O</code>’ when there is no default value: why not just ‘<code>o</code>’? Well, there is ‘<code>o</code>’ as well. Unlike <code>\newcommand</code>, <code>\NewDocumentCommand</code> can tell the difference between an option argument that is not given and one that is empty. To do that, it provides a test to see if the argument is empty:

<pre>\NewDocumentCommand\OneOptOfTwoWithTest{om}{%
  \IfNoValueTF{#1}
    {Do stuff with #2 only}
    {Do stuff with #1 and #2}%
}
</pre>

Don't worry if you forget to do the test: the special marker that is used here will simply print ‘-NoValue-’ as a reminder!

<h2>Two types of optional argument</h2>

Sometimes you might want two different optional arguments, and be able to tell which is which. This can be done by using something other than square brackets, often using angle brackets (‘&lt;’ and ‘&gt;’). We can do that using the letter ‘<code>d</code>’ (or ‘<code>D</code>’ if we give a default).

<pre>\NewDocumentCommand\TwoTypesOfOpt{D&lt;&gt;{}O{}m}%
  {Text using #1, #2 and #3}
</pre>

What input syntax does this make? Let's look at some examples

<pre>\TwoTypesOfOpt{text}             % One mandatory
\TwoTypesOfOpt[text]{text}       % A normal optional
\TwoTypesOfOpt&lt;text&gt;{text}       % A special optional
\TwoTypesOfOpt&lt;text&gt;[text]{text} % Both optionals
</pre>

How did that work? The first two characters after the ‘<code>D</code>’ are used to find the optional argument, so in this case ‘<code>&lt;</code>’ and ‘<code>&gt;</code>’.

<h2>Finding stars or other special markers</h2>

Another common idea in LaTeX is to use a star to indicate some special version of a macro. Creating those with <code>\newcommand</code> is difficult, but it is easy with <code>\NewDocumentCommand</code>

<pre>\NewDocumentCommand\StarThenArg{sm}{%
  \IfBooleanTF#1
    {Use #2 with a star}
    {Use #2 without a star}%
}
</pre>

Here, ‘<code>s</code>’ represents a star argument. You'll see that it ends up as <code>#1</code>, while the mandatory argument is <code>#2</code>. You'll also see that there needs to be a test to see if there is a star (<code>\IfBooleanTF</code>). This doesn't mention stars as the test can be used for other things.

<h2>Summing up</h2>

There is more to xparse than I've mentioned here, but I hope that this is a useful flavour of what it can be used for. To get more flexibility there is a bit more to think about compared to <code>\newcommand</code>, but the overall consistency is hopefully worth it.