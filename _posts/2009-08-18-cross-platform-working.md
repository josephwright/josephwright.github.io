---
id: 382
title: Cross-platform working
date: 2009-08-18T20:49:12+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=382
permalink: /2009/08/18/cross-platform-working/
categories:
  - General
tags:
  - 7-Zip
  - CTAN
  - Info-Zip
  - TDS
  - Unix
  - Windows
---
As many people will know, the <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a> team have come up with the idea of having TDS-ready zip files for packages. The idea is that you can just download the zip into your local TeX directory, unzip it and run texhash, with no TeX-based unpacking or document compilation.

That's all fine when it works, but I've recently had a bit of trouble making zips at my end. My favoured tool for doing that has tended to be <a title="7-Zip" href="http://www.7-zip.org">7-Zip</a>. However, it was pointed out to me last week that the resulting zip files are not quite right. On Unix systems, the command <code>unzip -xa</code> will convert line endings to the system convention (LF only), even if they come from Windows (LF-CR endings). However, this requires that the zip identifies text files, and 7-Zip marks everything as binary!

I did a bit of hunting around, and found <a title="Info-ZIP Homepage" href="http://www.info-zip.org">Info-ZIP</a>, where after a bit of hunting about you can find <code>zip</code> and <code>unzip</code> binaries for Windows. These give me Unix-like capabilities on Windows, so I can make the appropriate files, alter line endings on zipping/unzipping and check the results.

That led me to take another look at the batch file I use  each time I release something to CTAN: doing it by hand is an unreliable business!  I've reworked it quite a bit, to generalise everything and also add a few tweaks. For anyone interested, the file is <a href="http://www.texdev.net/wp-content/uploads/2009/08/make.bat">available here</a>. It's called make, so that you get Unix-like abilities on Windows. The file has to be customised for each package I write, but most of this version is generalised, and can be altered using a few settings.
<pre>set AUXFILES=aux cmds dvi glo gls hd idx ilg ind ist log los out tmp toc
set CLEAN=bib bst cls eps gz ins cfg pdf sty tex txt zip
set DOCEXTRA=\AtBeginDocument{\OnlyDescription}
set INDEXFILE=gglo
set PACKAGE=achemso
set PDF=%PACKAGE%
set TDSROOT=latex\%PACKAGE%
set TEX=achemso-demo
set TXT=README
set UNPACK=%PACKAGE%.dtx</pre>
Anyone at all familiar with batch files will see that this is a block of environmental variables: in this case, these are the settings for my <a title=" 	Support for American Chemical Society journal submissions" href="http://tug.ctan.org/cgi-bin/ctanPackageInformation.py?id=achemso">achemso</a> package. Most are pretty obvious settings, but in case anyone wants to use the file for their own purposes:
<ul>
	<li><code>AUXFILES</code> File types to delete after every run: throw away files.</li>
	<li><code>CLEAN</code> File types deleted only if make clean is run: useful stuff.</li>
	<li><code>DOCEXTRA</code> Inserted when creating documentation, can be anything. I don't typeset the code for my packages in the release documents, hence the <code>\OnlyDescription</code> setting.</li>
	<li><code>INDEXFILE</code> This is always <code>gglo</code> for documents using the <code>ltxdoc</code> class, but is <code>l3doc</code> if using the LaTeX3 class <code>l3doc</code>.</li>
	<li><code>PACKAGE</code> Pretty obvious, the bundle name!</li>
	<li><code>PDF</code> The names of PDF files to add to the documentation part of a TDS zip. By having this as a setting, special effects (demo documents, for example) are possible.</li>
	<li><code>TDSROOT.</code> Almost always as given for a LaTeX package.</li>
	<li><code>TEX</code> A list of .tex files to copy into the TDS archive: to avoid any testing files, not all .tex files are copied.</li>
	<li><code>TXT</code> The names of text files to copy to the documentation directory</li>
	<li><code>UNPACK</code> The file(s) to run to unpack the package. I use .dtx files that are self-extracting, but the traditional method is to have a separate .ins file.</li>
</ul>
If the batch file proves useful to enough people, I might write some proper documentation and do a bit more generalisation.

With all of that in place, I can hopefully keep Unix-based LaTeX users happy without too much work!