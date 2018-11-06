---
id: 347
title: Keyval methods in LaTeX3
date: 2009-07-13T20:25:32+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=347
permalink: /2009/07/13/keyval-methods-in-latex3/
categories:
  - LaTeX3
---
I've been working for a while on a method to provide a reasonably powerful method for creating keyval input for <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3</a>. This has been going under the working title “keys3”, but yesterday I took the plunge and added the code to the LaTeX3 <a title="LaTeX 3 development code" href="http://www.latex-project.org/code.html">development repository</a>. For the moment, this can only be accessed <em>via </em>SVN, but if the rest of the team are happy with the idea, it will appear in the next snap shot that is sent to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a>.

The ideas in the new module (now called <code>l3keys</code>) have been inspired by the <code><a title="Create PostScript and PDF graphics in TeX" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=pgf">pgfkeys</a></code> package. By using keyval methods to create keys, the idea is to make life a lot easier for the programmer. However, things are somewhat modified compared to the <code>pgfkeys</code> package, mainly to try to keep the input syntax simple but powerful enough for most uses. For example, there are separate functions for creating keys and setting them, an idea that all other keyval packages use. So a typical setup block might look like:
<pre>\keys_define:nn { module } {  
  key-one   .set:N     = \l_module_one_tl,   % Store input in variable
  key-one   .value_required:,
  key-two   .bool:N    = \l_module_two_bool, % Either true or false
  key-three .code:n    = { Code using an argument #1 },
  key-three .default:n = text
}</pre>
while keys are set using:
<pre>\keys_set:nn { module } {
  key-one = Value,
  key-two = true,
  key-three
}</pre>
Hopefully, the ideas are flexible and clear enough for people to get working with. One thing to notice: the key names are hyphenated. It looks like that will be the “style guide” suggestion for LaTeX3 keys. At some point, I'll look at writing a <a title="The Communications of the TeX Users Group" href="http://www.tug.org/TUGboat/"><em>TUGBoat</em></a> article on how everything works.
