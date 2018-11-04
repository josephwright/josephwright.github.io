---
id: 1726
title: 'Case changing: solving the challenges in TeX'
date: 2014-07-10T09:21:57+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1726
permalink: /2014/07/10/case-changing-solving-the-challenges-in-tex/
categories:
  - LaTeX3
tags:
  - Unicode
  - UTF-8
---
I wrote recently about <a href="http://www.texdev.net/2014/07/08/luatex-manipulating-utf-8-text-using-lua/">handling UTF-8 input in Lua</a>, and in particular the fact that doing text manipulation needs a bit of care. One area that I've been looking at recently is doing case changing operations. We've been looking at this for <code>expl3</code>, so I thought it would be worth looking at this in a bit of detail. I'm going to mainly focus on the <em>results</em> rather than <em>implementation</em>: the latter is important when it affects the output but not really otherwise (except for the team!).
<h2>Background</h2>
The first thing to think about is what case changing is needed for. We'll see in a bit that TeX uses 'case changing' for something very different from what we might think of as changing case in 'text'. First, though, let's look at what those 'normal' requirements are. The <a href="http://www.unicode.org/">Unicode Consortium</a> have looked in detail at this: take a look at <a href="http://www.unicode.org/versions/Unicode6.2.0/ch03.pdf">the standard</a> for all of the detail. The common situations are:
<ul>
 	<li>'Removing' the case from text to allow 'caseless' comparisons ('case-folding'). This is primarily used 'internally' by code, and tends traditionally to be handled by simply lower casing everything before some comparison. The Unicode approach has some slight differences between case-folding and lower-casing, but it's relatively straight-forward.</li>
 	<li>Upper-casing 'text'. Here, all characters that have a case mapping are changed to the upper-case versions. That's a relatively simple concept, but there is a bit more to it (as we'll see).</li>
 	<li>Title- or sentence-casing 'text'. The concept here is usually implemented by upper-casing the first character of a phrase, or of each word, then to lower-case the rest. Again, the Unicode specs have a bit more to say on this: there are some character(s) that should not be upper-cased at the start of a word in this context but need a special 'title-case' character. (For example, in Dutch 'IJ' at the start of words should both be upper-cased.)</li>
</ul>
Just to make life a bit more fun, there are also some language-dependent rules for case changing, and some places where the outcome of a case change depends on the context (sigma at the end of words is the most obvious example). So there are a few challenges if we want to cover all of this in TeX. We've also got to think about the 'TeX angle': what does 'text' mean, how do we handle math mode, <em>etc.</em>
<h2>TeX primitives</h2>
TeX provides two primitives for changing case, <code>\lowercase</code> and <code>\uppercase</code>. These are powerful operations, and in particular are very often used for something that's got very little to do with case at all: making characters with non-standard category codes. As that isn't a 'real' case change at all, I won't look at it further here, other than noting that it means we need those primitives for something even if we do case changing another way entirely!

Sticking with changing case of 'text', <code>\uppercase</code> and <code>\lowercase</code> rely on the fact that each character has a one-to-one mapping for upper- and lower-casing (defined by <code>\uccode</code> and <code>\lccode</code>). Assuming these are not 'do nothing' mappings, they allow a simple replacement of characters
<pre><code>\uppercase{hello} =&gt; HELLO
\lowercase{WORLD} =&gt; world
</code></pre>
With XeTeX and LuaTeX, these mappings are set up for all sensible UTF-8 codepoints ('characters'). However, the are one-to-one mapping with no context-awareness: that makes it impossible to cover some parts of the Unicode definitions I've mentioned (at least using the primitives directly). They also change everything in the input, which makes handling things like
<pre><code>\uppercase{Some text $y = mx + c$}
</code></pre>
a bit tricky (there are ways, of course!).

Another TeX concern is 'expandability': <code>\uppercase</code> and <code>\lowercase</code> are not expandable. That means that while we can do
<pre><code>\uppercase{\def\foo{some text}}
</code></pre>
and have <code>\foo</code> defined as <code>SOME TEXT</code>, the apparently 'obvious' alternative
<pre><code>\edef\foo{\uppercase{some text}}
</code></pre>
doesn't have the expected result (<code>\foo</code> here is defined as <code>\uppercase{some text}</code>). Moreover, it means we can't use the primitives inside places where TeX requires expansion. As a result, things like
<pre><code>\csname\lowercase{Some-input}\endcsname
</code></pre>
result in an error. Of course, there are always ways around the problem, but I think it looks a lot 'nicer' for the user if a way can be found to do these operations expandably. As we'll see in a bit, that is doable if we accept a few restrictions.
<h2>Case folding</h2>
If we want to implement case changing without using <code>\lowercase</code> and <code>\uppercase</code> then we have to have some form of iterative mapping over the 'text' input. Doing that while keeping the code expandable is doable if we accept a few restrictions, which I'll come to in a bit. One to mention now is that the code here assumes e-TeX is available and that we have the <code>\pdfstrcmp</code> primitive or equivalent functionality: pdfTeX, XeTeX and LuaTeX all cover these requirements.

For 'case-folding' we can make some simplifications which make this the most straight-forward situation to set up. First, case-folding is a one-to-one change with no context-dependence: nice and easy. Secondly, as this is needed only for 'internal' stuff and not for 'text' to be typeset we can assume that everything can be handled as a (TeX) string by applying <code>\detokenize</code>. That avoids issues with things like escaping math mode, brace groups and the like. Setting up an expandable mapping is then relatively straight-forward, and the issue becomes simply how do with actually change the case of each character.

With a list of over 1000 possible characters to case-fold, comparing each and every one to find a hit would get slow. Luckily, Bruno Le Floch spotted that we can divide up that long list into 'bite sized' chunks by using the last two digits of the character code of the input, giving 100 short lists, each of which is realistic just to look through. (For those interested in the internals, the final comparison is done using <code>\str_case:nnF</code>, which is an expandable string-based selection using <code>\pdfstrcmp</code>.)

Putting everything together lead to the documented interface
<pre><code>\str_fold_case:n { &lt;input&gt; }
</code></pre>
which does exactly what it says: folds the case of the input, which is treated as a string. The only real point to note here is that with pdfTeX it doesn't make sense to talk about UTF-8 as the engine doesn't support it. Thus the changes here are restricted to ASCII (A-Z): for a string that's clear, but life is a bit more murky for 'text' input. I'll come back to that below.
<h2>Case changing</h2>
Real case changing provides a few more challenges. Looking first at the Unicode definitions, there are both context- and language-dependent rules to worry about. It turns out that there are relatively few of these, so a bit of work with some hard-coding seems to cover most of them. That does require a bit of 'bending the rules' to fit in with how TeX parses stuff, so there may yet be more work to do here!

As we are now looking at text which might have a variety of TeX tokens in it then doing the mapping raises issues. It turns out that we can do an expandable mapping provided we accept that any brace groups end up with <code>{</code> and <code>}</code> as the grouping tokens even if that wasn't true to start with (a bit of an edge-case but we have to specify these things!). (Note that this does require both e-TeX and <code>\pdfstrcmp</code>, so it's not true for 'classical' TeX.) However, that raises an interesting issue: should stuff inside braces be case changed or not? At the moment, we've gone for 'no', as that's very much like the BibTeX approach
<pre><code>title = {Some text with including a {Proper-Name}}
</code></pre>
which also makes the code a bit easier to write. However, it's not quite clear if this is the best plan: I'll point to one open question below.

Another question is what category codes should apply in the <em>output</em>. For the folding case, it was easy: everything is treated as a string so the output is too. That's not the situation for general text, but at the same time it seems sensible to assume that you are case changing things that will be typeset ('letters'). Again, this is rather more of a concepts than a technical question.

Answering these questions, or at least taking a documented position on them, it's possible to define functions such as
<pre><code>\tl_lower_case:n { &lt;text&gt; }
\tl_upper_case:nn { &lt;language&gt; } { &lt;text&gt; }
</code></pre>
that implement the case changing I've outlines. As this is very much a 'work in progress' those names are not fixed: there's a feeling that perhaps <code>\text_...</code> might be more 'sensible' (the input should be 'well-behaved'). What's needed is some testing: we thing the idea is a good one, but at the moment it's not clear we've got all of the ideas right!

Notice the versions that know about languages: the idea is that these will get things like Turkish dotted/dotless-i correct. Of course, that assumes you know the language the input is in, but hopefully that's normally true!

One thing to note here is again the pdfTeX case. As we are dealing with 'engine native' input, it's only set up to do changes for the ASCII range. That's fine, but it leaves open the question of LICR text. For example,
<pre><code> \tl_upper_case:n { \'{e} }
</code></pre>
currently doesn't do anything as there are braces around the <code>e</code>. I'm not sure what's best: skipping brace groups is generally easier for the user, but they probably would be surprise by this outcome! (With XeTeX or LuaTeX, the input would hopefully be <code>é</code> so the problem doesn't arise.)
<h2>Conclusions</h2>
Case changing is a tricky thing to get right. We've made some progress in providing a 'clear' interface in <code>expl3</code> that can cover not only UTF-8 input but also language-dependence. What' needed now is some testing and feedback: we hope these things are useful!