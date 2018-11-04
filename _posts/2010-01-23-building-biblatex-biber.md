---
id: 611
title: Building biblatex-biber
date: 2010-01-23T20:24:56+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=611
permalink: /2010/01/23/building-biblatex-biber/
categories:
  - biblatex
  - Packages
tags:
  - biber
  - Perl
---
The <a title="Biber: A BibTeX replacement for users of biblatex" href="http://biblatex-biber.sourceforge.net/">biblatex-biber</a> project provides probably the best way for <a title="Bibliographies in LaTeX using BibTeX for sorting only" href="http://ctan.org/pkg/biblatex">biblatex</a> users to switch to pure UTF-8 bibliography information. However, getting it to build can cause problems: biblatex-biber is a <a title="The Perl Programming Language" href="http://www.perl.org/">Perl</a> programme, and needs various downloads from <a title="Comprehensive Perl Archive Network" href="http://www.cpan.org/">CPAN</a>. I thought it would therefore be useful to put some simple recipes here, explaining what I've done to get a working biblatex-biber on Windows, Ubuntu and Mac OS X. I'm assuming that the latest biblatex-biber release has been downloaded and unzipped somewhere, and that the Command Prompt/Terminal/Shell is open in that directory (folder).

<h2>Mac OS X 10.6 (Snow Leopard)</h2>

Mac OS X comes with Perl installed, so life is relatively easy. At the Terminal, you need to run the <code>cpan</code> script as root:

<pre>sudo cpan</pre>

The cpan script has its own prompt, but this is very similar to the Terminal one. First, I updated <code>cpan</code> itself and installed a helper module with

<pre>install CPAN
reload cpan
install YAML
</pre>

That done, the various requirements for biblatex-biber can be installed, using the single call

<pre>install Data::Dump List::AllUtils Readonly Text::BibTeX Readonly::XS</pre>

For the more cautious person (such as me), each <code>install</code> instruction can be given on a separate line: this keeps things a bit more controlled. I accepted the standard settings, except when asked about installing items that were only needed for testing, where I said no.

Once <code>cpan</code> has done all of the installing, you can leave it by typing

<pre>exit
</pre>

So now back at the Terminal prompt, a few simple instructions

<pre>perl Build.PL
./Build
sudo ./Build install</pre>

That put biblatex-biber onto the path for all users: everything then worked correctly.

<h2>Ubuntu 9.10</h2>

Once again, Perl is installed as standard in Linux distributions: I'm using <a title="Ubuntu Home Page" href="http://www.ubuntu.com/">Ubuntu</a> as a representative system. Before starting <code>cpan</code>, there is an additional step, which is to install an extra Ubuntu package. So at the Terminal, you need to do

<pre>sudo apt-get install libxml2-dev
</pre>

This is needed as otherwise you get some very odd errors in a bit. Now, essentially the same recipe works as for the Mac. First run <code>cpan</code> running and update and install <code>YAML</code>. Then there is a long list of items to install

<pre>install Data::Dump List::AllUtils Readonly Text::BibTeX Readonly::XS XML::Writer XML::LibXML File::Slurp</pre>

which can again be done one at a time, for the more cautious.

After exiting <code>cpan</code>, the same three lines at the Terminal should work as in the Mac section.

<pre>perl Build.PL
./Build
sudo ./Build install</pre>

<h2>Windows (XP, Vista and 7)</h2>

To date, my attempts to build biblatex-biber on Windows (using <a title="Strawberry Perl" href="http://strawberryperl.com/">Strawberry Perl</a>) have failed as I can't get the Perl module <code>Text::BibTeX</code> to install. This is supposed to be optional, but without it biblatex-biber does not seem to work, although I do get it to build. Luckily, there is a self-contained binary for Windows available from the project site. This includes its own Perl system, so there is no need to get Perl set up before trying it. Everything seems to work for me with this version. Any ideas on what is necessary would be helpful!