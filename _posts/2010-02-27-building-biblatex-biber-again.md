---
title: Building biblatex-biber (again)
layout: post
permalink: /2010/02/27/building-biblatex-biber-again/
categories:
  - biblatex
  - Packages
---
I [recently posted](/2010/01/23/building-biblatex-biber/) some information on building [`biblatex-biber`](http://biblatex-biber.sourceforge.net/). Since then, v0.5 of `biblatex-biber` has appeared and there are some positive changes. The code now creates its own file to grab the required Perl modules. So on Mac OS X (Snow Leopard) and Ubuntu (9.10) all I needed to do after downloading the source was

```bash
perl Build.PL
sudo ./Build installdeps
./Build
./Build test
sudo ./Build install
```

at the Terminal. The second step grabbed all of the modules needed and everything worked fine.

On Windows, life is still a bit complicated but I now can get things to work. A bit of a trawl on the Internet led to a [blog post about Text::BibTeX](http://blogs.perl.org/users/alberto_simoes/2010/02/textbibtex-040-released.html). At the moment, the solution is still in beta and so there is a bit of work to do. With [Strawberry Perl](http://strawberryperl.com/) installed I went to the Command Prompt (as Administrator) and started the `cpan` program. At its prompt I did

```bash
install Config::AutoConf Capture::Tiny IPC::Run
install A/AM/AMBS/Text/Text-BibTeX-0.40_3.tar.gz
```

which all seemed to work. After downloading and unzipping the source for `biblatex-biber` (which is in `.gz` format, so use something like [7-Zip](http://www.7-zip.org/) to open it), still as Administrator at the Command Prompt I did

```bash
perl build.pl
build installdeps
build
build test
build install
```

and everything worked. So I've finally got it working across all platforms. Hopefully the `Text::BibTeX` install will become easier when it moves from beta status.
