---
id: 819
title: When to use \protected
date: 2010-10-07T19:50:20+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=819
permalink: /2010/10/07/when-to-use-protected/
categories:
  - General
tags:
  - etex
  - protected
  - robust
---
ε-TeX introduced the idea of ‘protected’ macros over ten years ago, but many experienced (La)TeX users struggle with the concept. The idea of the \protected primitive is that it will prevent a macro being expanded inside an <code>\edef</code> or <code>\write</code>, so that
<pre>\protected\def\example{Hello}
\edef\test{\example}
\show\test</pre>
will give
<pre>\test=macro:
-&gt;\example .</pre>
Why would you want to do this? Well, there are some things that do not work properly inside an <code>\edef</code>. The classic one is an assignment: the following does not work
<pre>\edef\fails{\def\fails{stuff}}</pre>
This will give an undefined control sequence error for <code>\fails</code>, rather than carrying out in ‘inner’ <code>\def</code>. So as part of a general strategy I would recommend always making any macro that performs an assignment protected. That also applies if you know that one macro will use another that is itself protected. This is exactly what we've been doing in the work on <a href="http://www.latex-project.org/latex3.html">LaTeX3</a>, where the aim is that all macros are either protected or will expand safely inside an <code>\edef</code>. However, the idea applies more widely: making things protected is a lot more reliable than using LaTeX's ‘robust’ mechanism, and avoids some nasty errors. ε-TeX has been around long enough that there is no real excuse not to make use of this mechanism.