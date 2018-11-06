---
id: 1256
title: 'Programming LaTeX3: Token list variables'
date: 2011-12-26T12:19:31+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1256
permalink: /2011/12/26/programming-latex3-token-list-variables/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In the <a title="Programming LaTeX3: Category codes, tokens and token lists" href="http://www.texdev.net/2011/12/21/programming-latex3-category-codes-tokens-and-token-lists/">last post</a>, I talked about the concept of a token list and some general functions which act on token lists. That's fine if you just want to take some input and ‘do stuff’, but a very common requirement when programming is storing input, and for that we need variables. LaTeX3 provides a number of different types of variable: we'll start with perhaps the most general of all, the <em>token list variable</em>.
<h2>Token list variables</h2>
So what is a token list variable (‘<code>tl</code>’)? You might well guess from the name that its a way of storing a token list! As such, a <code>tl</code> can be used to hold just about anything, and indeed this means that several of the other variable types we'll meet later are <code>tl</code>s with a special internal structure.

Before we can save anything in a <code>tl</code>, we need to create the variable: this is a general principle of programming LaTeX3. We can then store something inside the variable by setting it:
<pre>\tl_new:N \l_mypkg_name_tl
\tl_set:Nn \l_mypkg_name_tl { Fred }</pre>
Hopefully, the analysis of this code is not too hard. First, <code>\tl_new:N</code> creates a new token list variable which I've called <code>\l_mypkg_name_tl</code>. (I'll explain how the naming works in a little while.) The second line will set the new <code>tl</code> to contain the text <code>Fred</code>. Assuming that the surrounding code has done nothing strange, we've stored four letter tokens in <code>\l_mypkg_name_tl</code>.

As I said, a <code>tl</code> can contain anything: we are not limited to letters. So
<pre>\tl_new:N \l_mypkg_other_tl
\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ ! }</pre>
is also perfectly-valid for the content of a token list variable (although whether we'll be able to use it safely is a different matter).
<h2>Variable naming and TeX's grouping system</h2>
From the <a title="Programming LaTeX3: Creating functions" href="http://www.texdev.net/2011/12/14/programming-latex3-creating-functions/">earlier discussion</a> of the way that functions are named in LaTeX3, it might be obvious that there is also a system to how variables are named. Skipping over the initial <code>\l_</code>, what we've got is a module name (<code>mypkg</code>), some further description of the nature of the variable (in this case <code>name</code>), and finally the variable type (<code>tl</code>), divided up by <code>_</code> in exactly the same way we did for functions. We'll see that other variables follow the same scheme.

So what's the leading <code>\l_</code> about? This tells us about the <em>scope</em> that we should use when setting the variable. As TeX is a macro expansion language, variables are not local to functions. However, they can be local to TeX groups, which are created in LaTeX3 using
<pre>\group_begin:
% Code here
\group_end:
</pre>
Setting a variable locally means that any changes stay within a group
<pre>\tl_new:N \l_mypkg_name_tl
\tl_set:Nn \l_mypkg_name_tl { Fred }
\group_begin:
  \tl_set:Nn \l_mypkg_name_tl { Ginger }
\group_end:
% \l_mypkg_name_tl reverts to 'Fred'
</pre>
On the other hand, we sometimes need <em>global</em> variables which ignore any groups
<pre>\tl_new:N \g_mypkg_name_tl
\tl_gset:Nn \g_mypkg_name_tl { Fred }
\group_begin:
  \tl_gset:Nn \g_mypkg_name_tl { Ginger }
\group_end:
% \g_mypkg_name_tl still 'Ginger'
</pre>
So the <code>\l_</code> or <code>\g_</code> tells you what scope the variable contents have, and whether you should <code>set</code> or <code>gset</code> it. (You can probably work out that <code>gset</code> means 'set globally'.)
<h2>Using the content of token list variables</h2>
Okay, putting stuff into token list variables is all very well and good, but unless we can do something with the content then it's not really that useful. Of course, we can do things with the content of variables. The most basic thing to do is simply to insert the content of the <code>tl</code> into the input that TeX is working with
<pre>\tl_use:N \l_mypkg_name_tl
</pre>
That's very handy, but we can also examine the content of a token list variable. For example, we saw before that <code>\tl_length:n</code> will produce the length of a token list, and we can do the same for a token list variable using <code>\tl_length:N</code>.
<pre>\tl_set:Nn \l_mypkg_name_tl { Fred }
\tl_length:N \l_mypkg_name_tl % '4'
</pre>
There's a lot more we can do with token list variables, but this post is already long enough, so I'll come back to more that we can do with them in the next post.
<h2>Tips for TeX programmers: the internals of token list variable</h2>
Experienced TeX programmers are probably wondered about token list variables, and in particular exactly what the underlying TeX structure is. A <code>tl</code> is just a macro that we are using as a variable rather than function. That should not be too much of a surprise, as storing tokens in macros is very much basic TeX programming. So <code>\tl_set:Nn</code> is almost the same as the <code>\def</code> primitive.

What might worry you slightly is that I said
<pre>\tl_new:N \l_mypkg_other_tl
\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ ! }</pre>
will work. That won't work with <code>\def</code>, and you'd normally expect to need a token register (<code>toks</code>) for this. However, we don't use <code>toks</code> for LaTeX3 programming at all, and that's because we require e-TeX. So
<pre>\tl_set:Nn \l_mypkg_other_tl { \ERROR ^ _ # $ ! }</pre>
is actually the same as
<pre>\edef \l_mypkg_other_tl { \unexpanded { \ERROR ^ _ # $ ! } }</pre>
which will allow us to put <em>any</em> tokens inside a macro.

The other thing you might notice is that I've said that <code>tl</code>s have to be declared, even though at a TeX level this is not the case. This is a principle of good LaTeX3 programming, and although it's not enforced as standard any non-declared token list variables are coding errors. You can test for this using
<pre>\usepackage[check-declarations]{expl3}</pre>
which uses some slow checking code to make sure that all variables are declared before they are used.
