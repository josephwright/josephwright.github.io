---
id: 1265
title: 'Programming LaTeX3: More on token list variables'
date: 2012-01-22T10:34:39+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1265
permalink: /2012/01/22/programming-latex3-more-on-token-list-variables/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In my <a title="Programming LaTeX3: Token list variables" href="http://www.texdev.net/2011/12/26/programming-latex3-token-list-variables/">previous post</a>, I introduced the idea of a <em>token list variable</em>, the LaTeX3 term for a macro used to store ‘stuff’. Token list variables (tl vars) are the basis of many of the higher level data types in LaTeX3, and they also have arbitrary contents. As a result, there are a lot of generic functions to do things with tl vars.
<h2>Adding content, changing content</h2>
A very common thing to do with stored material is either to add to it, which we can do either on the left or the right. The LaTeX3 functions to do this are called <code>\tl_put_left:Nn</code> and <code>\tl_put_right:Nn</code> (and so on), which makes it easy to build up complicated material quite quickly. So
<pre>\tl_new:N \l_my_a_tl
\tl_set:Nn \l_my_a_tl { stuff }
\tl_put_right:Nn \l_my_a_tl { ~here }
\tl_put_left:Nn \l_my_a_tl { My~ }
\tl_use:N \l_my_a_tl</pre>
will print ‘My stuff here’. That's easy enough to do without LaTeX3 coding, but find-and-replace is a bit more involved. So the functions

<code>\tl_replace_once:Nnn</code> and <code>\tl_replace_all:Nnn</code> are working a little harder:
<pre>\tl_set:Nn \l_my_a_tl { stuff~to~change }
\tl_replace_once:Nnn \l_my_a_tl { change } { alter }
\tl_use:N \l_my_a_tl % 'stuff to alter'
\tl_replace_all:Nnn \l_my_a_tl { t } { q }
\tl_use:N \l_my_a_tl % 'squff qo alqer'</pre>
<h2>Adding one tl var to another</h2>
So far, I've added literal input to tl vars. That's useful, but a very common task to to combine two or more variables together. To do that, we need a way to access the <em>content</em> of a variable. First, what doesn't work is doing
<pre>\tl_new:N \l_my_b_tl
\tl_set:Nn \l_my_a_tl { stuff }
\tl_set:Nn \l_my_b_tl { ~more~stuff }
\tl_put_right:Nn \l_my_a_tl { \l_my_b_tl }</pre>
as what ends up inside

<code>\l_my_a_tl</code> is <code>stuff\l_my_b_tl</code>. This is where LaTeX3's expansion control comes into play. So far, we've seen arguments of type <code>N</code> and <code>n</code>, but there are others. There are a number of other types, but I want here to introduce just one one: <code>V</code>. A <code>V</code>-type argument will pass the <em>value</em> of a variable, rather than its name. So the correct way to add the content of one token list variable to another is
<pre>\tl_set:Nn \l_my_a_tl { stuff }
\tl_set:Nn \l_my_b_tl { ~more~stuff }
\tl_put_right:NV \l_my_a_tl \l_my_b_tl</pre>
which results in <code>\l_my_a_tl</code> containing <code>stuff more stuff</code>. Now, the LaTeX3 kernel does not provide every possible combination of argument types (although it does provide <code>\tl_put_right:NV</code>). That's not a problem, as they can easily be created:
<pre>\cs_generate_variant:Nn \tl_put_right:Nn { NV }</pre>
This is a ‘soft’ process: if the variant requested already exists, nothing happens, but otherwise the variant is created. So provided the base function exists, you can always create any variants you need.
<h2>Mappings</h2>
Another key idea when working with tl vars is the ability to map to each token they contain. For that, there are again a couple of useful functions, <code>\tl_map_function:NN</code> and <code>\tl_map_inline:Nn</code>. The two differ mainly in <em>expandability</em>, a concept we've not covered just yet! I'll be coming back to that in a later post, so for the moment I'll just use <code>\tl_map_inline:Nn</code>. What does a mapping do? Try
<pre>\tl_set:Nn \l_my_a_tl { stuff }
\tl_map_inline:Nn \l_my_a_tl { I~saw~'#1'. \\ }</pre>
and you should get a listing of each separate token in the tl var:
<blockquote>I saw 's'. I saw 't'. I saw 'u'. I saw 'f'. I saw 'f'. As you can hopefully see, within the second argument of <code>\tl_map_inline:Nn</code> the place holder <code>#1</code> is used to insert a single token from the tl var. For a more complicated tl var</blockquote>
<pre>\tl_set:Nn \l_my_a_tl { { stuff } ~ { which } ~ is ~ { complicated } }
\tl_map_inline:Nn \l_my_a_tl { I~saw~'#1'. \\ }</pre>
we get
<blockquote>I saw 'stuff'. I saw 'which'. I saw 'i'. I saw 's'. I saw 'complicated'. So you'll see that spaces are ignored by the mapping, and that a brace group counts as a single item. I've not covered every token list and token list variable function, but hopefully the basic concepts are now laid out. In the next post, I'll move on to some other concepts, so that we can being to put more structures together.</blockquote>
