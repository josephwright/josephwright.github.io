---
id: 883
title: LaTeX3 and document environments
date: 2011-01-09T11:17:28+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=883
permalink: /2011/01/09/latex3-and-document-environments/
categories:
  - LaTeX3
tags:
  - environments
  - xparse
---
There was a <a href="http://tex.stackexchange.com/questions/8528/">question</a> on the <a title="{TeX} Q&amp;A" href="http://tex.stackexchange.com/">{TeX} Q&amp;A site</a> recently about compiling a document reading
<pre>\documentclass{minimal}
\document
a
\enddocument
</pre>
This doesn't work: I've explained why as my answer to the question. I also mentioned that in <a title="The LaTeX3 project" href="http://www.latex-project.org/latex3.html">LaTeX3</a> I'd expect this won't work. Here, I want to look at that in a bit more detail.

First, the background. When LaTeX2e creates an environment <code>foo</code>, what actually happens is two macros called <code>\foo</code> and <code>\endfoo</code> are defined (hence the original question). When you do
<pre>\begin{foo}
...
\end{foo}
</pre>
LaTeX looks for the <code>\foo</code> macro, and if it finds it starts a group and inserts <code>\foo</code>. At the end of the environment, LaTeX will use <code>\endfoo</code> if it exists, but this is not required.

There are some problems with this scheme. First, it's possible to abuse the system, as something like
<pre>\begin{emph}
...
\end{emph}
</pre>
will not raise an error even though <code>\emph</code> was never intended to be used as the start of an environment. (LaTeX2e does not require that <code>\endemph</code> exists here: it's only the start of an environment which must be defined.) Secondly, due to this mixing it's not possible to have a <code>foo</code> environment and independent <code>\foo</code> macro: the two are tied together. Finally, as <code>\endfoo</code> is ‘special’ <code>\newcommand</code> won't let you create macros which start <code>\end...</code>.

For LaTeX3, we want the approach to be different. Document commands and document environments should be independent of one another, and so <a href="http://ctan.org/pkg/xparse">xparse</a> defines a pair of special internal macros when you use
<pre>\NewDocumentEnvironment{foo}...
</pre>
This is totally independent of a macro called <code>\foo</code>, so the plan is that you'll be able to have an environment called <code>foo</code> and a separate <code>\foo</code> command, or indeed one called <code>\endfoo</code>.

At present, most people will be using xparse with LaTeX2e. That means we still need to follow what LaTeX2e does. So at the moment you're not going to see the change: messing with the LaTeX2e mechanism looks like a very bad idea. However, for a native LaTeX3 format the clash will disappear.