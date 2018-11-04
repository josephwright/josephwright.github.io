---
id: 643
title: Building biblatex-biber (again)
date: 2010-02-27T07:55:12+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=643
permalink: /2010/02/27/building-biblatex-biber-again/
categories:
  - biblatex
  - Packages
---
I <a href="http://www.texdev.net/2010/01/23/building-biblatex-biber/">recently posted</a> some information on building <a title="A BibTeX replacement for biblatex users" href="http://biblatex-biber.sourceforge.net/">biblatex-biber</a>. Since then, v0.5 of biblatex-biber has appeared and there are some positive changes. The code now creates its own file to grab the required Perl modules. So on Mac OS X (Snow Leopard) and Ubuntu (9.10) all I needed to do after downloading the source was
<pre>perl Build.PL
sudo ./Build installdeps
./Build
./Build test
sudo ./Build install
</pre>
at the Terminal. The second step grabbed all of the modules needed and everything worked fine.

On Windows, life is still a bit complicated but I now can get things to work. A bit of a trawl on the Internet led to a <a href="http://blogs.perl.org/users/alberto_simoes/2010/02/textbibtex-040-released.html">blog post about Text::BibTeX</a>. At the moment, the solution is still in beta and so there is a bit of work to do. With <a title="Strawberry Perl" href="http://strawberryperl.com/">Strawberry Perl</a> installed I went to the Command Prompt (as Administrator) and started the <code>cpan</code> program. At its prompt I did
<pre>install Config::AutoConf Capture::Tiny IPC::Run
install A/AM/AMBS/Text/Text-BibTeX-0.40_3.tar.gz</pre>
which all seemed to work. After downloading and unzipping the source for biblatex-biber (which is in .gz format, so use something like <a title="7-Zip" href="http://www.7-zip.org/">7-Zip</a> to open it), still as Administrator at the Command Prompt I did
<pre>perl build.pl
build installdeps
build
build test
build install
</pre>
and everything worked. So I've finally got it working across all platforms. Hopefully the Text::BibTeX install will become easier when it moves from beta status.