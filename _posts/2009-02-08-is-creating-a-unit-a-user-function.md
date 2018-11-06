---
id: 168
title: 'Is creating a unit a &#8220;user&#8221; function?'
date: 2009-02-08T19:29:22+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=168
permalink: /2009/02/08/is-creating-a-unit-a-user-function/
categories:
  - Packages
  - siunitx
---
Working on<a title="siunitx version 2" href="http://siunitx.berlios.de"> siunitx version 2</a>, I'm confronted with a slight problem.  Currently, the macros used to manipulate units are called
<ul>
	<li><code>\newunit</code></li>
	<li><code>\renewunit</code></li>
	<li><code>\provideunit</code></li>
</ul>
which follows the LaTeX 2ε <code>\newcommand</code>, <em>etc.</em>; the same is true for prefixes and so forth.  These names were probably not the best choice: for example, <a title="biblatex on CTAN" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=biblatex">biblatex</a> also has a <code>\newunit</code> macro (although there is not a clash, luckily).

I've been thinking of better names, but I'm not sure whether these should be document level (all lower-case), or design level (mixed upper-case and lower-case). Some ideas:
<ol>
	<li><code>\DeclarePhysicalUnit</code> (create without checks)</li>
	<li><code>\NewPhysicalUnit</code> (create with checks: would require <code>\RenewPhysicalUnit</code>, <em>etc.</em>)</li>
	<li><code>\NewUnit</code> (as 2 but shorter)</li>
	<li><code>\newphysicalunit</code> (as 2 but document level)</li>
	<li><code>\createphysicalunit</code> (is “create” better than “new”?)</li>
	<li><code>\createunit</code> (avoids the confusion with biblatex)</li>
</ol>
You'll see that I've not included “SI” in any of the above: it looks odd, and of course you can create non-SI units anyway.  How do other people see this?
