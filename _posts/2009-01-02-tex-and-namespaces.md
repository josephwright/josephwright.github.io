---
id: 61
title: TeX and namespaces
date: 2009-01-02T13:24:37+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=61
permalink: /2009/01/02/tex-and-namespaces/
categories:
  - LaTeX3
---
A question on the <a title="LaTeX3 Homepage" href="http://www.latex-project.org/latex3.html">LaTeX3 mailing list</a> has got me thinking abut namespaces. Plain TeX users tend to have their own set of macros, plus those from the plain format, and so are pretty much in control of everything. On the other hand, <a title="Pragma, the home of ConTeXt" href="http://www.pragma-ade.com/">ConTeXt</a> users can rely on the small focussed development team to keep naming sensible. That leaves LaTeX, where things are complicated.

The current LaTeX situation is rather a hodge-podge of approaches. Internal macros follow the plain TeX conventions, and include one or more <code>@</code> symbols. However, this is all rather a mess, as there is no real system: <code>\@tf@r</code>, from the kernel, for example. What is it for (no peeking)? User macros are little better, with some including package names, some with captials, others defined only in certain places, etc. This means developing a new package is something of a risk: it is very easy to end up getting e-mails saying
<blockquote>Your package XXX clashes with package YYY because both define \SomeObsureMacroName. Sort it out!</blockquote>
or words to that effect.
<h2>LaTeX3 approaches</h2>
The LaTeX3 “module” concept helps to some extent. This formalises what many package authors do in LaTeX2e, so that <em>all</em> internal macros for a module (a package for LaTeX3) start with <code>\module</code> (or some fixed abbreviation for the module name). However, this leaves two issues:
<ol>
 	<li>How are module names managed?</li>
 	<li>What about user macros?</li>
</ol>
It we imagine that LaTeX3 will eventually have a large community of developers, in the same way as LaTeX2e does, then this needs to be addressed. The ConTeXt approach of of small, focussed team doesn't really apply in the LaTeX world.
<h2>Ideas</h2>
I'd suggest a two-part solution to the issue, first at the LaTeX level and then pre-emptively using a database. At the LaTeX level, I'd suggest that each module should include two special functions, one to reserve the module name and a second to reserve user macro names. Something like:
<pre>\module_details:n { % Note _ and : are "letters"
  prefix     = &lt;prefix&gt;,
  full~name  = &lt;Long macro name&gt;, % ~ is a space
  version    = &lt;version&gt;,
  date       = &lt;date&gt;,
  maintainer = &lt;Whoever&gt;,
  e-mail     = &lt;contact e-mail&gt;, % and so on
}
\module_reserve_names:n  {
  &lt;function-name-1&gt;,
  &lt;function-name-2&gt;, % etc.
}</pre>
You'd do this at the start of the module, and a check could then be made with other modules that had already been loaded. In the event of a clash, LaTeX could then give a useful error message including the name of the clashing module, and hopefully contact details.

The second part of the system would be to encourage people to submit this information to a central database, so that developers can check in advance of writing anything. I'd imagine you'd put the details above in a separate file, and upload only this data (lets call it a .mod file). It should then be relatively easy to parse the information out into a mySQL database, and hopefully some PHP would produce a simple interface for checking. Two methods would be available: check against the database (hopefully early on in the process of writing a module) and submitting to the database for inclusion. I'd hope most of this could be automated (he says with no experience at all!).
<h2>Conclusion</h2>
TeX doesn't help out much in keeping a large namespace in order. So you either have to have a very small team (the ConTeXt approach), keep the namespace small (the plain TeX approach) or seek for your own system (where LaTeX3 are going). LaTeX3 doesn't quite cover everything at the moment, but the potential is there.