---
id: 1668
title: The beamer slide overlay concept
date: 2014-01-17T20:06:14+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1668
permalink: /2014/01/17/the-beamer-slide-overlay-concept/
categories:
  - beamer
tags:
  - overlays
---
There was a <a href="http://tex.stackexchange.com/questions/154521">question recently</a> on the <a href="http://tex.stackexchange.com">TeX StackExchange site</a> about the details of how slide overlays work in the <a href="http://ctan.org/pkg/beamer"><code>beamer</code></a> class. The question itself was about a particular input syntax, but it prompted me to think that a slightly more complete look at overlays would be useful.

A word of warning before I start: don't overdo overlays! Having text or graphics appear or disappear on a slide can be useful but is easy to over-use. I'm going to focus on the mechanics here, but that doesn't mean that they should be used in every <code>beamer</code> frame you create.
<h2>Overlay basics</h2>
Before we get into the detail of how <code>beamer</code> deals with overlays, I'll first give a bit of background to what they are. The <code>beamer</code> class is built around the idea of frames:
<pre><code>\begin{frame}
  \frametitle{A title}
  % Frame content
\end{frame}
</code></pre>
which can produce one or more slides: pages of output that will appear on the screen. These separate slides within a frame are created using overlays, which is the way the <code>beamer</code> manual describes the idea of having the content of individual slides varying. Overlays are 'contained' within a single frame: when we start a new <code>frame</code>, any overlays from the previous one stop applying.

The most basic way to create overlays is to explicitly set up individual items to appear on a particular slide within the frame. That's done using the (optional) overlay argument that <code>beamer</code> enables for many document components: this overlay specification is given in angle brackets. The classic example is a list, where the items can be made to appear one at a time.
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;1-&gt; This is on the first and all following slides
    \item&lt;2-&gt; This is on the second and all following slides
    \item&lt;3-&gt; This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
As you can see, the overlay specification here is simply the first slide number we want the item to be on followed by a <code>-</code> to indicate 'and following slides'. We can make things more specific by giving only a single slide number, giving an ending slide number and so on.
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;1&gt; This is on the first only
    \item&lt;-3&gt; This is on the first three slides
    \item&lt;2-4,6&gt; This is on the second to fourth slides and the sixth slide
  \end{itemize}
\end{frame}
</code></pre>
The syntax is quite powerful, but there are at least a couple of issues. First, the slide numbers are hard-coded. That means that if I want to add something else in before the first item I've got to renumber everything. Secondly, I'm having to repeat myself. Luckily, <code>beamer</code> offers a way to address both of these concerns.
<h2>Auto-incrementing the overlay</h2>
The first tool <code>beamer</code> offers is the the special symbol <code>+</code> in overlay specifications. This is used as a place holder for the 'current overlay', ans is automatically incremented by the class. To see it in action, I'll rewrite the first overlay example without any fixed numbers.
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;+-&gt; This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
What's happening here? Each time <code>beamer</code> finds an overlay specification, it automatically replaces all of the <code>+</code> symbols with the current overlay number. It then advances the overlay number by 1. So in the above example, the first <code>+</code> is replaced by a <code>1</code>, the second by a <code>2</code> and the third by a <code>3</code>. So we get the same behaviour as in the hard-coded case, but this time if I add another item at the start of the list I don't have to renumber everything.

There are of course a few things to notice. The first overlay in a frame is number 1, and that's what <code>beamer</code> sets the counter to at the start of each frame. To get the second item in the list to appear on slide 2, we still require an overlay specification for the first item: although I used one, I could have skipped the <code>&lt;1-&gt;</code> in the hard-coded example and nothing would have changed. The second point is that <em>every</em> <code>+</code> in an overlay specification gets replaced by the same value. We'll see later there are places you might accidentally add a <code>+</code> to mean 'advance by 1': don't do that!
<h2>Reducing redundancy</h2>
Using the <code>+</code> approach has made our overlays flexible, but I've still have to be repetitive. Handily, <code>beamer</code> helps out there too by adding an optional argument to the list which inserts an overlay specification for each line:
<pre><code>\begin{frame}
  \begin{itemize}[&lt;+-&gt;]
    \item This is on the first and all following slides
    \item This is on the second and all following slides
    \item This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
Notice that this is needs to be inside the 'normal' <code>[ ... ]</code> set up for an optional argument. Applying an overlay to every item might not be exactly what you want: you can still override individual lines in the standard way.
<pre><code>\begin{frame}
  \begin{itemize}[&lt;+-&gt;]
    \item This is on the first and all following slides
    \item This is on the second and all following slides
    \item This is on the third and all following slides
    \item&lt;1-&gt; This is on the first and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
Remember not to overdo this effect: just because it's easy to reveal every list line by line doesn't mean you should!
<h2>Repeating the overlay number</h2>
The <code>+</code> syntax is powerful, but as it always increments the overlay number it doesn't allow us to remove the hard-coded numbers from a case such as
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;1-&gt; This is on the first and all following slides
    \item&lt;1-&gt; This is also on the first and all following slides
    \item&lt;2-&gt; This is on the second and all following slides
    \item&lt;2-&gt; This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
For this case, <code>beamer</code> offers another special symbol: <code>.</code>.
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;.-&gt; This is also on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;.-&gt; This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
What happens here is that <code>.</code> can be read as 'repeat the overlay number of the last <code>+</code>'. So the two <code>+</code> overlay specifications create two slides, while the two lines using <code>.</code> in the specification 'pick up' the overlay number of the preceding <code>+</code>. (The <code>beamer</code> manual describes the way this is actually done, but I suspect that's less clear than thinking of this as a repetition!)

Depending on the exact use case, you might want to combine this with the 'reducing repeated code' optional argument, with <code>&lt;.-&gt;</code> as an override.
<pre><code>\begin{frame}
  \begin{itemize}[&lt;+-&gt;]
    \item This is on the first and all following slides
    \item&lt;.-&gt; This is also on the first and all following slides
    \item This is on the second and all following slides
    \item&lt;.-&gt; This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
<h2>Offsets</h2>
A combination of <code>+</code> and <code>.</code> use can be used to convert many 'hard-coded' overlay set ups into 'relative' ones, where the slide numbers are generated by <code>beamer</code> without you having to work them out in advance. However, there are cases it does not cover. To allow even more flexibility, <code>beamer</code> has the concept of an 'offset': and adjustment to the number that is automatically inserted. Offset values are given in parentheses after the <code>+</code> or <code>.</code> symbol they apply to, for example
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+(1)-&gt; This is on the second and all following slides
    \item&lt;+(1)-&gt; This is on the third and all following slides
    \item&lt;+-&gt; This is also on the third and all following slides
  \end{itemize}
\end{frame}
</code></pre>
Notice that in this adjustment only applies to the substitution, so both the second and third lines above end up as <code>&lt;3-&gt;</code> after the automatic replacement. If you try the demo, you'll also notice that none of the items appear on the first slide!

Perhaps a more realistic example for where an offset is useful is the case of revealing items 'out of order', where the full list makes sense in some other way. With hard-coded numbers this might read
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;1-&gt; This is on the first and all following slides
    \item&lt;2-&gt; This is on the second and all following slides
    \item&lt;1-&gt; This is on the first and all following slides
    \item&lt;2-&gt; This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
which can be made 'flexible' with a set up such as
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    \item&lt;.(-1)-&gt; This is on the first and all following slides
    \item&lt;.-&gt; This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
or the equivalent
<pre><code>\begin{frame}
  \begin{itemize}
    \item&lt;+-&gt; This is on the first and all following slides
    \item&lt;.(1)-&gt; This is on the second and all following slides
    \item&lt;.-&gt; This is on the first and all following slides
    \item&lt;+-&gt; This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
</code></pre>
As shown, we can use both positive and negative offsets, and these work equally well for <code>+</code> and <code>.</code> auto-generated values. You have to be slightly careful with negative offsets, as while <code>beamer</code> will add additional slides for positive offsets, if you offset below a final value of <code>0</code> then errors will crop up. With this rather advanced set up, which version is easiest for you to follow will be down to personal preference.

Notice that positive offsets <em>do not</em> include a <code>+</code> sign: remember what I said earlier about <em>all</em> <code>+</code> symbols being replaced. If you try something like <code>&lt;+(+1)&gt;</code>, your presentation will compile but you'll have a <em>lot</em> of slides!
<h2>Summary</h2>
The <code>beamer</code> overlay specific can help you set up complex and flexible overlays to generate slides with dynamic content. By using the tools carefully, you can make your input easier to read and maintain.