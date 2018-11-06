---
id: 732
title: siunitx version 2 released
date: 2010-05-23T18:57:01+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=732
permalink: /2010/05/23/siunitx-version-2-released/
categories:
  - LaTeX3
  - Packages
  - siunitx
---
After many months of work, I'm pleased to announce that I've just sent version 2 of <a title="A comprehensive (SI) units package" href="http://ctan.org/pkg/siunitx">siunitx</a> to CTAN. Many readers will be familiar with the package and some of the development process. Here, I've put together a summary as ‘release notes’ for the new version.

<h2>A comprehensive (SI) units package</h2>

Typesetting values with units requires care to ensure that the combined mathematical meaning of the value plus unit combination is clear. In particular, the SI units system lays down a consistent set of units with rules on how these are to be used. However, different countries and publishers have differing
conventions on the exact appearance of numbers (and units).

The siunitx package provides a set of tools for authors to typeset numbers and units in a consistent way. The package has an extended set of configuration options which make it possible to follow varying typographic conventions with the same input syntax. The package includes automated processing of numbers and
units, and the ability to control tabular alignment of numbers.

<h2>Version 2</h2>

Over the past two years siunitx has developed to include many features not originally foreseen when development began. While it has been possible to add a range of new features, some of the underlying limitation of the version 1 code have made this difficult. At the same time, renewed effort by the LaTeX Team on the development of <a title="LaTeX3 Project" href="http://www.latex-project.org/latex3.html">LaTeX3</a>, and in particular the <a title="Packages supporting LaTeX3 programming conventions" href="http://ctan.org/pkg/l3kernel">expl3</a> programming system, has offered a more robust method to create the internal structure of siunitx. As a result, version 2 of siunitx has been almost completely re-written internally.

As well as fixing a number of bugs and limitations in the original release, version 2 is also much better written to work quickly. As a result, most users should see performance enhancements with this new release of siunitx.

As part of the revision of siunitx, the option system and user macros have been completely re-thought. The options now have longer, descriptive names and also a much clearer range of input values. The options which in version 1 took either a key word or a literal value have been replaced by ones which take literals only: in some cases this means that advice has been added to the documentation on how to get particular output effects.

<h2>Moving from version 1 to version 2</h2>

Depending on how you use siunitx, there may be very little to do to move to version 2. The new version includes a compatibility support file, meaning that loading siunitx using:

<pre>\usepackage[load-configurations = version-1]{siunitx}</pre>

should mean that existing documents compile with very few changes.

There are some changes to standard settings between version 1 and version 2, which may lead to some alterations in documents. At the same time, a small number of the features of siunitx version 1 which I feel did not work cleanly have been dropped. At present, some of these are scheduled to be re-examined for
inclusion in later releases of siunitx.

While there is a back-compatibility layer for users upgrading, it is strongly recommended that documents are updated to use the new option names and functions. The new approach has been chosen as it is an improvement on the previous version, and in the longer term this layer may be removed.

<h2>Installation</h2>

Most users will obtain siunitx as part of their TeX distribution. <a title="MiKTeX" href="http://www.miktex.org/">MiKTeX 2.8</a> should include siunitx version 2 after a short delay (a few days after CTAN upload). For <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> users, there will be a slight delay as the package will appear in updated form in TeX Live 2010 but not TeX Live 2009 (which is frozen).

For users who wish to install siunitx themselves, the package is available as a pre-extracted zip file, <a href="http://mirror.ctan.org/install/macros/latex/contrib/siunitx.tds.zip">siunitx.tds.zip</a>. Simply unzip this in your local texmf directory and run ‘<code>texhash</code>’ to update the database of file locations. Version 2 of siunitx requires up to date versions of the LaTeX3 packages expl3 and xpackages. These are also available from <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org/">CTAN</a> in ready to install format (as <a href="http://mirror.ctan.org/install/macros/latex/contrib/l3kernel.tds.zip">expl3.tds.zip</a> and <a href="http://mirror.ctan.org/install/macros/latex/contrib/l3packages.tds.zip">xpackages.tds.zip</a>), and can be installed in the same way if necessary.

If you want to unpack the dtx yourself, running ‘<code>tex siunitx.dtx</code>’ will extract the package whereas ‘<code>latex siunitx.dtx</code>’ will extract it and also typeset the documentation. Typesetting the documentation requires a number of packages in addition to those needed to use siunitx. These should all be available in a complete TeX Live 2010 or MiKTeX 2.8 installation.

<h2>Development code and bug database</h2>

In order to help users see what is happening, and also to allow me to work efficiently, the development code for siunitx is available on the code hosting site <a title="siunitx repository on BitBucket " href="http://github.com/josephwright/siunitx">BitBucket</a>.

You can download the very latest code from there: of course, this may or may not work properly depending on exactly what I have added to the code.

The BitBucket site includes an <a href="http://github.com/josephwright/siunitx/issues">issue tracker</a>, where you can report bugs or make feature requests. I also add bugs to the database from e-mails I get from users. Filling in the bug database helps to make sure that I do not forget things, and also helps other users see what issues are known.

If you want to contribute code to siunitx, you can of course send patches directly to me. Alternatively, the code is hosted using the revision control system Mercurial, which was chosen as it is decentralised and is easy to install on a range of operating systems (I use MacOS X, Windows XP, Windows 7 and Ubuntu!). I'm happy to explain to potential contributors how Mercurial works for developing siunitx.

<h2>Roadmap for future releases</h2>

The bug database already includes a number of feature requests which are <a href="http://github.com/josephwright/siunitx/issues?milestone=v2.1">marked to be looked at for version 2.1</a>. The current intention is that the next few months will be devoted to bug fixes in this release (v2.0), with moves to add features for v2.1 beginning in the late summer. I anticipate that v2.1 will be released toward the end of 2010.

It is likely that not all of the features currently marked as to be looked at for v2.1 will be fully working by the time it is released. At the same time, there are some longer term areas which may also need attention. Version 2.2 of siunitx is therefore planned, but with no current list of features marked for inclusion. This version is likely to appear in Spring 2011.

One longer term aim is to include LuaTeX support in siunitx, so that the entire package can work much more rapidly with LuaTeX than when using TeX macros alone. This is not likely to happen until next year (2011), but is in the bug database and is part of the longer term development plan for siunitx.

<h2>The internals of siunitx</h2>

Currently, the only documented interface to any of the functionality of siunitx is via the key-value control system and functions described in the manual. The internal code of the package is not documented, and there is therefore no guarantee of stability of internal functions. While it is common for users to have to modify the internals of LaTeX2e packages as part of their documents, this is not good programming practice and is not encouraged for siunitx, or indeed in general.

If there is a user function that you require that is not available using the documented tools, please either e-mail or report a bug in the database. One of the general aims of siunitx is to provide a proper documented interface for all of the
functions of the package. I am therefore very happy to add interfaces to internal processes as necessary.

Programmers should note that siunitx is coded using the LaTeX3 'expl3' programming system. This looks somewhat different to traditional TeX or LaTeX programming. Details of the programming environment are documented as part of the expl3 bundle. Currently, none of the internal functions or interfaces are documented, and so are not meant for use outside of siunitx. Other programmers wanting to make use of internal siunitx functions are encouraged to get in contact with me. This will enable me to ensure that the parts of siunitx which are needed by others are documented and are not changed without consultation.
