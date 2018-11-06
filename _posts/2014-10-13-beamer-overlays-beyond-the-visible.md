---
id: 1759
title: Beamer overlays beyond the \visible
date: 2014-10-13T20:00:31+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1759
permalink: /2014/10/13/beamer-overlays-beyond-the-visible/
categories:
  - beamer
  - Packages
---
I wrote earlier this year about <a href="http://www.texdev.net/2014/01/28/the-overlay-syntax-and-pause-in-beamer/">using the <code>beamer</code> overlay concept with relative slide specifications</a> to produce dynamic slide structures. Another <a href="http://tex.stackexchange.com/questions/205625/">question about overlays</a> came up recently on TeX StackExhange, but this time wanting to do something a bit different.

The 'standard' <code>beamer</code> overlay system does the same as the <code>\visible</code> command: makes things appear and disappear, but always keeps space for them on the slide. However, <code>beamer</code> also provides <code>\only</code>, which completely omits items not visible on a slide. So the question was how to combine this idea with the general overlay concept.

It turns out that this is all quite straight-forward if you know what to look for. The standard <code>beamer</code> overlay syntax, for example
<pre><code>\item&lt;+-&gt;
</code></pre>
extends to include an action type to specify what the overlay should do. That is given as a keyword and an <code>@</code> before the overlay number(s). So for example
<pre><code>\begin{itemize}
  \item First item
  \item&lt;only@1&gt; Second item
  \item&lt;only@2&gt; Replacement second item
...
</code></pre>
will show <code>Second item</code> on the first slide then replace it entirely with <code>Replacement second item</code> on the second slide. That approach can be combined with the idea of relative slide specs, as I talked about before, to give something like
<pre><code>\documentclass{beamer}
\begin{document}
   \begin{frame}
   \begin{itemize}[&lt;+-&gt;]
      \item item 1
      \item item 2
      \item&lt;only@+-.(2)&gt; item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
</code></pre>
to have the 'normal' items appear one at a time but with <code>item 3</code> only on slides 3 and 4.

This doesn't just apply to <code>only</code>: other keywords that work here include <code>visible</code> and <code>alert</code>. The latter tends to be seen with another syntax element: <code>|</code> to separate out appearance from a second action. A classic example of that is
<pre><code>\documentclass{beamer}

\begin{document}
   \begin{frame}
   \begin{itemize}[&lt;+-&gt;]
      \item item 1
      \item item 2
      \item&lt;+-|alert@+(1)&gt; item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
</code></pre>
where <code>item 3</code> appears on the third slide and is highlighted on the fourth one. (Note that both <code>+</code> substitutions in this line use the <em>same</em> value for the pause counter, hence needing the <code>(1)</code> offset.) That's useful even without the 'one at a time' effect, with for example
<pre><code>\documentclass{beamer}

\begin{document}
   \begin{frame}
   \begin{itemize}
      \item item 1
      \item item 2
      \item&lt;alert@+(1)&gt; item 3
      \item item 4
      \item item 5
   \end{itemize}

   \end{frame}
\end{document}
</code></pre>
highlighting the item on the second slide.

A bit of imagination with this syntax can cover almost any appearance/disappearance/highlight requirement. As I said before: the key thing is not to overdo it!
