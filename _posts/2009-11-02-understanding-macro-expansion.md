---
id: 530
title: Understanding macro expansion
date: 2009-11-02T20:38:57+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=530
permalink: /2009/11/02/understanding-macro-expansion/
categories:
  - General
---
I get the occasional e-mail asking me to explain who some complex macro works. I usually answer by trying to show how I go about understanding things. There are a few simple steps:
<ol>
	<li>Start from the definition of the first macro you want to understand.</li>
	<li>From the definition, work out what arguments it will take (easy if they are not delimited).</li>
	<li>Replace every parameter in the definition by what you picked up in (2). Don't worry if things seem like they will change part way through: TeX has to fill in every #1, #2, <em>etc</em>. at the point of expansion.</li>
	<li>Now work through the expansion systematically. If you come to another macro, replace it by it's expansion (remembering any arguments), if you hit a primitive, work out what it will do, <em>etc</em>.</li>
	<li>It's important not to get confused by things that are redefined themselves during the expansion. TeX uses whatever the current meaning is when it expands/executes a token. So it's often useful to keep notes on definitions, <em>etc</em>., and check against them.</li>
</ol>
Usually, with a bit of care and some notes, enlightenment will dawn.
