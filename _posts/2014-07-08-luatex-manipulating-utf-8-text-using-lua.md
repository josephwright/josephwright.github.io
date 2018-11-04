---
id: 1720
title: 'LuaTeX: Manipulating UTF-8 text using Lua'
date: 2014-07-08T13:01:54+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1720
permalink: /2014/07/08/luatex-manipulating-utf-8-text-using-lua/
categories:
  - General
tags:
  - Lua
  - LuaTeX
  - Unicode
  - UTF-8
---
<p>Both the XeTeX and LuaTeX engines are natively UTF-8, which makes input of non-ASCII text a lot easier than with pdfTeX (certainly for the programmer: <code>inputenc</code> hides a lot of complexity for the end user!). With LuaTeX, there is the potential to script in Lua as well as program in TeX macros, and that of course means that you might well want to do manipulation of that UTF-8 input in Lua. What might then catch you out is that it's not quite as simple as all that!</p>

<p>Lua itself can pass around arbitrary bytes, so input in UTF-8 won't get mangled. However, the basic string functions provided by Lua are <em>not</em> UTF-8 aware. The LuaTeX manual cautions</p>

<blockquote>
  <p>The <code>string</code> library functions <code>len</code>, <code>lower</code>, <code>sub</code>, etc. are not UNICODE-aware.</p>
</blockquote>

<p>As a result, applying these functions to anything outside the ASCII range is not a good idea. At best you might get unexpected output, so</p>

<pre><code>tex.print (string.lower ("Ł"))
</code></pre>

<p>simply prints in <code>Ł</code> (with the right font set up). Worse, get an error as for example</p>

<pre><code>tex.print (string.match ("Ł","[Ł]"))
</code></pre>

<p>results in</p>

<pre><code>! String contains an invalid utf-8 sequence.
</code></pre>

<p>which is not what you want!</p>

<p>Instead of using the <code>string</code> library, the current correct approach here is to use <code>slnunicode</code>. Again, the LuaTeX manual has some advice:</p>

<blockquote>
  <p>For strings in the UTF-8 encoding, i.e., strings containing characters above code point 127, the corresponding functions from the <code>slnunicode</code> library can be used, e.g., <code>unicode.utf8.len</code>, <code>unicode.utf8.lower</code>, etc.</p>
</blockquote>

<p>and indeed</p>

<pre><code>tex.print(unicode.utf8.lower("Ł"))
</code></pre>

<p>does indeed print <code>ł</code>. There are still a few things to watch, though. The LuaTeX manual warns that <code>unicode.utf8.find</code> returns a byte range and that <code>unicode.utf8.match</code> and <code>unicode.utf8.gmatch</code> fall back on non-Unicode behaviour when an empty capture (<code>()</code>) is used. Both of those can be be allowed for, of course: they should not be big issues.</p>

<p>There's still a bit of complexity for two reasons. First, there's not really much documentation on the <code>slnunicode</code> library, so beyond trying examples it's not so easy to know what 'should' happen. For example, case-changing in Unicode is more complex than a simple one-to-one mapping, and can have language-dependencies. I'll probably return to that in another post for a TeX (or at least XeTeX/LuaTeX) take on this, but in the Lua context the problem is it's not so clear quite what's available! In a way, the second point links to this: the LuaTeX manual tells us</p>

<blockquote>
  <p>The <code>slnunicode</code> library will be replaced by an internal UNICODE library in a future LuaTeX version.</p>
</blockquote>

<p>which of course should lead to better documentation but at the price of having to keep an eye on the situation.</p>

<p>Over all, provided you are aware that you have to think, using Lua with Unicode works well, it's just that it's not quite as obvious as you might expect!</p>
