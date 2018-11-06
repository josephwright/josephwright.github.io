---
id: 674
title: 'siunitx version 2: beta release'
date: 2010-04-26T08:31:09+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=674
permalink: /2010/04/26/siunitx-version-2-beta-release/
categories:
  - Packages
  - siunitx
---
Over the past few months I've been working a new version of <a title="A comprehensive (SI) units package" href="http://tug.ctan.org/pkg/siunitx">siunitx</a> with completely re-written internals. This is now at the point where I hope that it is usable for most people, but before replaced version 1 some testing is needed. This is what this beta (testing) release is for. There are some important notes for people testing, which I'll run through below. For the impatient, you can get:
<ul>
	<li><a href="http://www.texdev.net/wp-content/uploads/2010/04/siunitx.tds.zip">A ready to install .zip file</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2010/04/siunitx.pdf">The documentation</a></li>
	<li><a href="http://www.texdev.net/wp-content/uploads/2010/04/siunitx.dtx">The source (dtx) file</a></li>
</ul>
<h2>Release notes</h2>
The code used in siunitx relies on the <a href="http://www.latex-project.org/">LaTeX3 Project</a> packages <a href="http://tug.ctan.org/pkg/expl3">expl3</a> and <a href="http://tug.ctan.org/pkg/xpackages">xpackages</a>. You will need the latest versions of both of these to test siunitx 2: they can both be downloaded from <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a> or installed using the update facilities in <a href="http://www.tug.org/texlive/">TeX Live</a> or <a href="http://www.miktex.org/">MiKTeX</a>.

Version 2 of siunitx renames most of the package options to make them more informative. The old names are available by using:
<pre>\usepackage[load-configurations = version-1]{siunitx}
</pre>
The new option names are intended to make it easier to continue to expand siunitx without having completely opaque option names. At the same time, the nature of some of the options has been changed. This means that there are no longer any ‘magic’ keywords, which have caused confusion in the past.

There will be no significant features added to siunitx version 2 between the beta version and the production release (probably in June). The aim is to get the inevitable bugs in the current code found and fixed, which is best done while not making other changes.

A small number of features from version 1 of siunitx are not present in version 2. The features removed have never worked as well as I would like, and so I felt it was better to remove them and rework them later if needed. If this causes severe problems for users then some of these decisions may of course be reversed.

I have had a large number of feature requests for siunitx, and only some of these have been added to version 2 at present. This is partly as I have a limited amount of time, and need to get siunitx 2 to release within a reasonable time. At the same time, some of the feature requests are very specialist and I need to consider which of these fall within the scope of the package. That said, I intend to work on adding more features to siunitx after the full release of version 2.0. More details on this will be posted here in the future.

Feedback on any aspect of siunitx version 2 is very welcome: <a href="mailto:joseph.wright@morningstar2.co.uk">joseph.wright@morningstar2.co.uk</a>.
