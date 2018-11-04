---
id: 1094
title: LaTeX3 Roadmap
date: 2011-09-05T09:45:17+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1094
permalink: /2011/09/05/latex3-roadmap/
categories:
  - LaTeX3
---
One of the questions that <a title="LaTeX3: More use, more work" href="http://www.texdev.net/2011/09/01/latex3-more-use-more-work/">comes up from time to time</a> is what the ‘roadmap’ is for LaTeX3 development. While there is not an official plan, I certainly have some ideas on what I'd like to see addressed in a concrete way. This is all rather flexible, but I'll try to outline some areas for attention.

<h2>Short term</h2>

The short term is about things which LaTeX3 does not critically depend on, and for which a lot of work is already done. This is very much an ongoing area:  small improvements spread across a range of topics. These items all fit into the concept of ‘LaTeX3 in LaTeX2e’, where this material can be loaded without affecting existing documents.

<h3>Floating point expressions</h3>

The current floating point implementation in LaTeX3 is based on carrying out assignments, and is pretty simple-minded in the way values are stored. Bruno Le Floch is working on an <a href="https://github.com/latex3/latex3/blob/master/l3kernel/l3fp.dtx">improved approach</a>, which will allow floating point expressions to be parsed in an expandable way. This will be very handy for doing things like box rotations, but also in the future for <a href="http://ctan.org/pkg/pgf">Tikz</a>-like drawing capabilities.

<h3>Extending key–value concepts</h3>

The current <a href="https://github.com/latex3/svn-mirror/blob/master/l3kernel/l3keys.dtx">l3keys</a> module is based loosely on <a href="http://ctan.org/pkg/pgf">pgfkeys</a>. One area that is not implemented is the idea of a ‘key path’. Using a path model for setting keys has some advantages, so I'd like to add something like the ability to do

<pre>\keys_set:n
  {
    /module .cd ,
    key-a = value ,
    key-b .meta = { key-a = setting , /other-module/key = value }
  }</pre>

<h3>LaTeX3 niggles</h3>

There are a <a href="https://github.com/latex3/svn-mirror/issues?sort=created&amp;direction=desc&amp;state=open">number of issues</a> that have come up as LaTeX3 has seen more use. Fixing these is an ongoing problem, and we should probably look to deal with a few over the coming weeks. The supply is not going to run out!

<h3>Documentation improvements</h3>

A key aim for LaTeX3 is to document all of the material which is intended for others to use. Getting documentation right is hard, and so another ongoing area is to improve the documentation. We've already done a bit of work on this, but it's certainly not complete.

<h2>Medium term</h2>

The medium term is about bigger ideas, but ones where there is some code written and we can see that results will appear within the next few months. These areas need discussion as much as writing code. Here, we move away from ‘LaTeX3 in LaTeX2e’ to code which will break existing documents unless they are adapted.

<h3>The galley</h3>

The galley is the vertical area into which text and other content is places. Galley management in LaTeX2e is basic, and this leads to odd effects with vertical spacing. For example, try

<pre>\end{itemize}
\vspace{3 pt}
\begin{itemize}</pre>

and see that you get 12 pt of space! We've already got three galley implementations, and are now working on a fourth! So the issue here is deciding what is the best approach: the different versions all have different levels of complexity. Hopefully we can resolve these ideas into a single working module within the next couple of months.

<h3>Font selection</h3>

The ‘New Font Selection Scheme’ in LaTeX2e is a pretty good approach to selecting fonts. So the first task here is more-or-less to convert the code to LaTeX3 syntax. There are then a few items to address, such as how to deal with small caps. Loading fonts also needs to be fitted in here: some combination of <a href="http://ctan.org/pkg/fontspec">fontspec</a> (for XeTeX and LuaTeX) with the existing pdfTeX mechanisms is going to be needed, and it's a question of how to do this.

<h2>Long term</h2>

The long-term is again about big ideas, but here ones where the code is not yet written. Some of the concepts are sorted, but beyond that there is work to do.

<h3>The output routine</h3>

The biggest single challenge for LaTeX3 at an implementation level is getting the output routine right. Here, we have <a href="https://github.com/latex3/svn-mirror/tree/master/xpackages/xor">xor</a>, an approach written by Frank Mittelbach. This works, but it's in need of a serious overhaul as the code has developed over many years. So at the moment it's rather a mix of LaTeX2e and LaTeX3 stuff. We've also got to discuss how the output routine should work, addressing things like flowing text across frames, grid typesetting and so on. This is all hard work.

<h3>Beyond the output routine</h3>

Once we have all of the above addressed, then we need to look at getting a format created that can actually typeset material. That means building the code level, galley, fonts and output routine into a stand-alone format. The result won't be impressive, as it won't have much in the way of mark-up abilities. However, it will allow testing without LaTeX2e. That's the stage where we'll need to add things like sectioning, float management, and all of the other stuff that can be done by LaTeX at the moment.