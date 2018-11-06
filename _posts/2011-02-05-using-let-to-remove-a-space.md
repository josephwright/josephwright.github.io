---
id: 909
title: Using \let to remove a space
date: 2011-02-05T07:39:27+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=909
permalink: /2011/02/05/using-let-to-remove-a-space/
categories:
  - General
---
On the <a href="http://tex.stackexchange.com/">{TeX} Q&amp;A site</a>, there was a question recently about <a href="http://tex.stackexchange.com/questions/10210/">splitting the first token off a list</a>, with the requirement that spaces are not skipped. In my answer, I've used \let to remove one space. The question is how to do this. Normally, if you want to use <code>\let</code> you do
<pre>\let\TokenA\TokenB
</pre>
In this case, TeX will skip spaces after <code>\let</code> and <code>\TokenA</code>, so we can't use it to <code>\let</code> to a space. However, what we can do is notice that TeX allows us to have an optional <code>=</code> followed by one space in the syntax for <code>\let</code>. We also need to make sure that TeX does not discard two spaces in the early stage of parsing, so can use <code>\@firstonone</code>:
<pre>
\@firstofone{\let\TokenA= }
</pre>
This will <code>\let</code> <code>\TokenA</code> to the next token in the input, even if it is a space. I've used this to remove the next token from some input in combination with <code>\afterassignment</code>:
<!-- {% raw %} -->
<pre>
\long\def\firstofone#1{#1}
\def\GobbleExactlyOne{%
  \afterassignment\NextThing
  \firstofone{\let\TokenA= }%
}
</pre>
<!-- {% endraw %} -->
Not something you need every day, but worth knowing about I think.
