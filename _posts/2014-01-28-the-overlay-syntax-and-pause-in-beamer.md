---
id: 1676
title: The +-overlay syntax and \pause in beamer
date: 2014-01-28T07:16:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1676
permalink: /2014/01/28/the-overlay-syntax-and-pause-in-beamer/
categories:
  - beamer
tags:
  - overlays
---
In a <a href="http://www.texdev.net/2014/01/17/the-beamer-slide-overlay-concept/">recent post</a> I looked at how to use the <code>+</code> syntax to create flexible overlays in <code>beamer</code>. The key concept of that syntax is to allow dynamic slides to be created without having to hard-code slide numbers. The classic example is to reveal a list an item at a time:
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
As I discussed in the earlier post, this is a very powerful way to create overlays (dynamic slides from the same frame source). However, a classic problem people have is combining this with the <code>\pause</code> command. For example, the following creates <em>four</em> slides:
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
  \pause
  Text after the list
\end{frame}
</code></pre>
Why? If you read the <code>beamer</code> manual, it's all about the value of <code>\beamerpauses</code>, but if we skip to the key point, you <em>should not</em> use <code>\pause</code> on the same slide as <code>&lt;+-&gt;</code> (or similar).
<h2>Beyond the power of <code>\pause</code>: <code>\onslide</code></h2>
The reason people get into trouble is I think because they imagine <code>\pause</code> as the best way to break 'running text' in a frame into overlays. However, <code>\pause</code> is really just the most basic way of breaking up frames and is meant just for the simplest cases
<pre><code>\begin{frame}
  Some content
  \pause
  Some more content
\end{frame}
</code></pre>
The moment you introduce other dynamic behaviour, you need more control than <code>\pause</code> offers. Indeed, this is pretty clear in the <code>beamer</code> manual: what people are actually looking for is <code>\onlside</code>.

Unlike <code>\pause</code>, which only knows some basic stuff about slide numbers, <code>\onslide</code> works with the full power of the flexible overlay specification (indeed, an overlay specification is required). So to get text after a list, what is needed is
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
  \onslide&lt;+-&gt;
  Text after the list
\end{frame}
</code></pre>
As we are then using the special <code>+</code> syntax for all of the overlays, everything is properly tied together and will give the (probably) expected result: three slides.

The <code>beamer</code> manual covers other more complex effects using <code>\only</code>, <code>\uncover</code>, <code>\alt</code> and so on, but using <code>\onslide</code> you can do everything you <em>think</em> you can do with <code>\pause</code> but actually have it work when using the <code>+</code> syntax on the slide too!