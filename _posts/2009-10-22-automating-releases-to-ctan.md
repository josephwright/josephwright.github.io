---
title: Automating releases to CTAN
layout: post
permalink: /2009/10/22/automating-releases-to-ctan/
categories:
  - General
---
I've talked in recent posts about various aspects of creating LaTeX packages, focussing on the dtx format. One thing I've been promising to cover is automating the release of material to [CTAN](https://www.ctan.org). Even for a basic package, there are a few files to sort out (the source, a readme file, the documentation and an ins file). For the documentation, you need to typeset the correct version, include the changes and code index. So even in a simple case, a bit of help from the computer is a good thing: I manage to miss stuff quite happily even with some stuff set up.

What do I mean by automation? Well, there is typesetting to do, files to copy and zip files to create. For Windows users, there are also line endings to worry about: CTAN prefer Unix ones for plain text files. All of that can be rolled up into some kind of script (a shell script on Unix or a batch file on Windows). Unix users also have easy access to the ‘make’ utility. The basic tasks are the same whatever method you go for, but I'm going to assume batch files for Windows and make files for Unix (including Mac OS X).

The aim here is not to have to most sophisticated system possible, but to make life easier. So I've not necessarily made every refinement I've thought of as some of them make what is going on much less clear. I'd also point out that a lot of the ideas here are ones I've adapted from elsewhere, or that have been suggested to me. Not much originality, but again that is not the main point. One thing to point out is that I've provided settings for copying dtx, ins, sty and pdf files. Other file types would need to be added, but hopefully there is enough here for the pattern to be clear without over-complicating things. You can always add things to a script so that the do nothing if they are not needed. So the same ideas can be used for packages with different requirements, with only a few basic settings to change.

The two files I'm going to provide both aim to give the same functionality: I work with both Windows and Unix, so I need that. As well as being able to clean out the working directory and make documentation, there are also methods to make a CTAN archive and a TDS one (to send to users for direct installation). Finally, I've included a local installation option: useful if you don't update your TeX system regularly and need your own code to be up to date!

## Windows batch files

A batch file on Windows (or indeed a shell script on Unix) is simply a list of commands you could type yourself at the command line, but with some flow control added.  Recent versions of Windows include a number of extensions beyond the old DOS capabilities: I'm going to use some of these, but that only rules out very old systems so it should be reasonably safe. If you want to grab the entire file in one go, it's [available here](/wp-content/uploads/2009/10/make.bat).

One problem is that there is no command line tool for creating zip files installed by default in Windows. I've tried a few out, and the best seems to be [Info-ZIP](http://www.info-zip.org/). It does a good job of marking up binary and text files, and also includes some abilities to sort out line endings. If it doesn't work for you, other tools such as the [Swiss File Knife](http://stahlforce.com/dev/index.php?tool=sfk) do the same thing on a file-by-file basis. Whatever you decide, it's best to put the support tools on the Windows path somewhere.

```bat
@echo off

  if not "%1" == "" goto :init

:help

  echo.
  echo  make clean        - delete all generated files
  echo  make ctan         - create an archive ready for CTAN
  echo  make doc          - typesets documentation
  echo  make localinstall - extract packages
  echo  make tds          - create a TDS-ready archive
  echo  make unpack       - extract packages

  goto :EOF

:init

  setlocal

  rem The name of the package to create should be set here: here, the
  rem example package "demopkg" is in use

  set PACKAGE=demopkg

  rem It is possible to unpack dtx files without needing any extra files, but
  rem some people prefer a separate ins file (or there may be no unpacking
  rem to do). This should be set up here: for a self-extracting dtx the
  rem standard setting is fine.

  set UNPACK=%PACKAGE%.dtx

  rem A list of pdf files to be typeset and included in the archive files
  rem created. The files named here will be typeset (looking for source files
  rem in the order .dtx, .tex, .ltx).

  set INCLUDEPDF=%PACKAGE%

  rem Plain text files to be included in the archives: the .txt extension is
  rem automatically stripped when creating the archive.

  set INLCUDETXT=README

  rem Files to typeset

  rem The settings for cleaning up after compilation are divided into two
  rem parts. AUXFILES are deleted after each (La)TeX run, CLEAN only
  rem when the user calls "make clean"

  set AUXFILES=aux dvi glo gls hd idx ilg ind ist log out toc
  set CLEAN=gz ins pdf sty tex txt zip

  rem Sets the order for searching for source files for pdfs

  set PDFSOURCES=dtx tex

  rem The file types for inclusion in the archive files: note that a CTAN
  rem archive should not contain "unpacked" files. Typeset files and their
  rem sources are not inlcuded here: they are dealt with separately

  set CTANFILES=dtx ins pdf
  set TDSFILES=%CTANFILES% sty

  rem Locations for building archives

  set CTANROOT=ctan
  set CTANDIR=%CTANROOT%\%PACKAGE%
  set TDSROOT=tds

  cd /d "%~dp0"

:main

  if /i "%1" == "clean"        goto :clean
  if /i "%1" == "ctan"         goto :ctan
  if /i "%1" == "doc"          goto :doc
  if /i "%1" == "help"         goto :help
  if /i "%1" == "localinstall" goto :localinstall
  if /i "%1" == "tds"          goto :tds
  if /i "%1" == "unpack"       goto :unpack

  goto :help

:clean

  echo.
  echo Deleting files

  for %%I in (%CLEAN%) do (
    if exist *.%%I del /q *.%%I
  )

  for %%I in (%TXT%) do (
    if exist %%I del /q %%I
  )

:clean-aux

  for %%I in (%AUXFILES%) do (
    if exist *.%%I del /q *.%%I
  )

  goto :end

:ctan

  call :zip
  if errorlevel 1 goto :EOF

  call :doc
  if errorlevel 1 goto :EOF

  echo.
  echo Creating archive

  for %%I in (%SOURCES%) do (
    xcopy /q /y %%I "%CTANDIR%\" &gt; nul
  )
  for %%I in (%CTANFILES%) do (
    xcopy /q /y *.%%I "%CTANDIR%\" &gt; nul
  )
  for %%I in (%INLCUDETXT%) do (
    xcopy /q /y %%I.txt "%CTANDIR%\" &gt; nul
    ren "%CTANDIR%\%%I.txt" %%I
  )

  pushd "%CTANROOT%"
  %ZIPEXE% %ZIPFLAG% %PACKAGE%.zip .
  popd
  copy /y "%CTANROOT%\%PACKAGE%.zip" &gt; nul

  rmdir /s /q %CTANROOT%

  goto :end

:doc

  call :unpack

  set SOURCES=

  for %%I in (%INCLUDEPDF%) do (
    for %%J in (%PDFSOURCES%) do (
      echo.
      if exist %%I.%%J call :typeset-%%J %%I.%%J
    )
  )

  goto :clean-aux

:file2tdsdir

  set TDSDIR=

  if /i "%~x1" == ".dtx" set TDSDIR=source\latex\%PACKAGE%
  if /i "%~x1" == ".ins" set TDSDIR=source\latex\%PACKAGE%
  if /i "%~x1" == ".pdf" set TDSDIR=doc\latex\%PACKAGE%
  if /i "%~x1" == ".sty" set TDSDIR=tex\latex\%PACKAGE%
  if /i "%~x1" == ".txt" set TDSDIR=doc\latex\%PACKAGE%

  goto :EOF

:localinstall

  call :unpack

  echo.
  echo Installing

  if not defined TEXMFHOME set TEXMFHOME=%USERPROFILE%\texmf

  for %%I in (%TDSFILES%) do (
    call :localinstall-int *.%%I
  )

  goto :end

:localinstall-int

  call :file2tdsdir %1

  if defined TDSDIR (
    xcopy /q /y %1 "%TEXMFHOME%\%TDSDIR%\" &gt; nul
  ) else (
    echo Unknown file type "%~x1"
  )

  goto :EOF

:tds

  call :zip
  if errorlevel 1 goto :EOF

  call :doc
  if errorlevel 1 goto :EOF

  echo.
  echo Creating archive

  for %%I in (%SOURCES%) do (
    call :tds-int %%I
  )
  for %%I in (%TDSFILES%) do (
    call :tds-int *.%%I
  )
  for %%I in (%INLCUDETXT%) do (
    call :tds-txt %%I
  )

  pushd "%TDSROOT%"
  %ZIPEXE% %ZIPFLAG% %PACKAGE%.tds.zip .
  popd
  copy /y "%TDSROOT%\%PACKAGE%.tds.zip" &gt; nul

  rmdir /s /q "%TDSROOT%"

  goto :end

:tds-int

  call :file2tdsdir %1

  if defined TDSDIR (
    xcopy /q /y %1 "%TDSROOT%\%TDSDIR%\" &gt; nul
  ) else (
    echo Unknown file type "%~x1"
  )

  goto :EOF

:tds-txt

  call :file2tdsdir %1.txt

  if defined TDSDIR (
    xcopy /q /y %1.txt "%TDSROOT%\%TDSDIR%\" &gt; nul
    ren "%TDSROOT%\%TDSDIR%\%1.txt" %1
  ) else (
    echo Unknown file type "%~x1"
  )

  goto :EOF

:typeset-dtx

  echo Typesetting %1

  pdflatex -interaction=nonstopmode -draftmode "\AtBeginDocument{\OnlyDescription}\input %1" &gt; nul
  if ERRORLEVEL 1 (
    echo ! Compilation failed
  )

  makeindex -q -s gglo.ist -o %~n1.gls %~n1.glo &gt; nul
  makeindex -q -s gind.ist -o %~n1.ind %~n1.idx &gt; nul
  pdflatex -interaction=nonstopmode "\AtBeginDocument{\OnlyDescription} \input %1" &gt; nul
  pdflatex -interaction=nonstopmode "\AtBeginDocument{\OnlyDescription} \input %1" &gt; nul

  goto :EOF

:typeset-tex

  echo Typesetting %1

  set SOURCES=%SOURCES% %1

  pdflatex -interaction=nonstopmode -draftmode %1 &gt; nul
  if ERRORLEVEL 1 (
    echo ! Compilation failed
  )
  pdflatex -interaction=nonstopmode %1 &gt; nul
  pdflatex -interaction=nonstopmode %1 &gt; nul

  goto :EOF

:unpack

  echo.
  echo Unpacking files

  for %%I in (%UNPACK%) do (
    tex %%I &gt; nul
  )

  goto :end

:zip

  if not defined ZIPFLAG set ZIPFLAG=-r -q -X -ll

  if defined ZIPEXE goto :EOF

  for %%I in (zip.exe "%~dp0zip.exe") do (
    if not defined ZIPEXE if exist %%I set ZIPEXE=%%I
  )

  for %%I in (zip.exe) do (
    if not defined ZIPEXE set ZIPEXE="%%~$PATH:I"
  )

  if not defined ZIPEXE (
    echo.
    echo This procedure requires a zip program,
    echo but one could not be found.
    echo
    echo If you do have a command-line zip program installed,
    echo set ZIPEXE to the full executable path and ZIPFLAG to the
    echo appropriate flag to create an archive.
    echo.
  )

  goto :EOF

:end

  shift
  if not "%1" == "" goto :main
```

Most of the ideas here should be pretty straight-forward. The clever part is `:file2tdsdir`, which I have to say was not my idea at all! It allows the batch file to ‘know’ which type of files go where, so that you only need the information once for use in several places.

To use the file, just alter the settings at the beginning. The pattern should be pretty clear, and most of the rest of the code (for example, `:file2tdsdir` for correctly placing files) is also quite obvious.

## Unix make files

Unix make files work somewhat differently to shell scripts. Each entry is a ‘target’, which is a file to create. I'm not going to explain in detail how they work, but in essense there are a series of fake ‘files’ which are the names of the settings you send to make (for example, `make ctan` needs a target called `ctan`). As with the batch file, there are a series of blanks to fill in here to customise things. I'm also sticking with the idea that things are pretty basic: a dtx file, a sty file and some documentation, plus perhaps one or more example tex files. Hopefully the idea is pretty clear. By keeping as much as possible in variables, the idea is to avoid needing to change the bulk of the file to move from one package to another. As with the batch file, the entire thing is [available here](/wp-content/uploads/2009/10/Makefile). to download.

```make
################################################################
################################################################
# Makefile for demopkg                                         #
################################################################
################################################################

################################################################
# Default with no target is to give help                       #
################################################################

help:
	@echo ""
	@echo " make clean               - clean out test directory"
	@echo " make ctan                - create a CTAN-ready archive"
	@echo " make doc                 - typeset documentation"
	@echo " make localinstall        - install files in local texmf tree"
	@echo " make tds                 - create a TDS-ready archive"
	@echo " make unpack              - extract packages"
	@echo ""

##############################################################
# Master package name                                        #
##############################################################

PACKAGE = demopkg

##############################################################
# Directory structure for making zip files                   #
##############################################################

CTANROOT := ctan
CTANDIR  := $(CTANROOT)/$(PACKAGE)
TDSDIR   := tds

##############################################################
# Data for local installation and TDS construction           #
##############################################################

INCLUDEPDF  := $(PACKAGE)
INCLUDETEX  :=
INCLUDETXT  := README
PACKAGEROOT := latex/$(PACKAGE)

##############################################################
# Details of source files                                    #
##############################################################

DTX      = $(PACKAGE).dtx
DTXFILES = $(PACKAGE)
UNPACK   = $(PACKAGE).dtx

##############################################################
# Clean-up information                                       #
##############################################################

AUXFILES = \
	aux  \
	glo  \
	gls  \
	hd   \
	idx  \
	ilg  \
	ind  \
	log  \
	out  \
	tmp  \
	toc  

CLEAN = \
	gz  \
	ins \
	pdf \
	sty \
	tex \
	txt \
	zip

################################################################
# File buiding: default actions                                #
################################################################

%.pdf: %.dtx
	NAME=`basename $&lt; .dtx` ; \
	echo "Typesetting $$NAME" ; \
	pdflatex -draftmode -interaction=nonstopmode "\AtBeginDocument{\OnlyDescription} \input $&lt;" &amp;&gt; /dev/null ; \
	if [ $$? = 0 ] ; then  \
	  makeindex -s gglo.ist -o $$NAME.gls $$NAME.glo &amp;&gt; /dev/null ; \
	  makeindex -s gind.ist -o $$NAME.ind $$NAME.idx &amp;&gt; /dev/null ; \
	  pdflatex -interaction=nonstopmode "\AtBeginDocument{\OnlyDescription} \input $&lt;" &amp;&gt; /dev/null ; \
	  pdflatex -interaction=nonstopmode "\AtBeginDocument{\OnlyDescription} \input $&lt;" &amp;&gt; /dev/null ; \
	else \
	  echo "  Complilation failed" ; \
	fi ; \
	for I in $(AUXFILES) ; do \
	  rm -f $$NAME.$$I ; \
	done

################################################################
# User make options                                            #
################################################################

.PHONY = \
	clean        \
	ctan         \
	doc          \
	localinstall \
	tds          \
	unpack

clean:
	echo "Cleaning up"
	for I in $(AUXFILES) $(CLEAN) ; do \
	  rm -f *.$$I ; \
	done
	rm -rf $(CTANROOT)/
	rm -rf $(TDSDIR)/

ctan: doc
	echo "Creating CTAN archive"
	mkdir -p $(CTANDIR)/
	rm -rf $(CTANDIR)/*
	cp -f *.dtx $(CTANDIR)/ ; \
	cp -f *.ins $(CTANDIR)/ ; \
	for I in $(INCLUDEPDF) ; do \
	  cp -f $$I.pdf $(CTANDIR)/ ; \
	done ; \
	for I in $(INCLUDETEX); do \
	  cp -f $$I.tex $(CTANDIR)/ ; \
	done ; \
	for I in $(INCLUDETXT); do \
	  cp -f $$I.txt $(CTANDIR)/; \
	  mv $(CTANDIR)/$$I.txt $(CTANDIR)/$$I ; \
	done ; \
	cd $(CTANDIR) ; \
	zip -ll -q -r -X $(PACKAGE).zip .
	cp $(CTANDIR)/$(PACKAGE).zip ./
	rm -rf $(CTANROOT)/

doc: $(foreach FILE,$(INCLUDEPDF),$(FILE).pdf)

localinstall: unpack
	echo "Installing files"
	TEXMFHOME=`kpsewhich --var-value=TEXMFHOME` ; \
	rm -rf $$TEXMFHOME/tex/$(PACKAGEROOT)/*.* ; \
	cp *.sty $$TEXMFHOME/tex/$(PACKAGEROOT)/ ; \
	texhash &amp;&gt; /dev/null

tds: doc
	echo "Creating TDS archive"
	mkdir -p $(TDSDIR)/
	rm -rf $(TDSDIR)/*
	mkdir -p $(TDSDIR)/doc/$(PACKAGEROOT)/
	mkdir -p $(TDSDIR)/tex/$(PACKAGEROOT)/
	mkdir -p $(TDSDIR)/source/$(PACKAGEROOT)/
	cp -f *.dtx $(TDSDIR)/source/$(PACKAGEROOT)/ ; \
	cp -f *.ins $(TDSDIR)/source/$(PACKAGEROOT)/ ; \
	for I in $(INCLUDEPDF) ; do \
	  cp -f $$I.pdf $(TDSDIR)/doc/$(PACKAGEROOT)/ ; \
	done ; \
	cp -f *.sty $(TDSDIR)/tex/$(PACKAGEROOT)/ ; \
	for I in $(INCLUDETEX); do \
	  cp -f $$I.tex $(TDSDIR)/doc/$(PACKAGEROOT)/ ; \
	done ; \
	for I in $(INCLUDETXT); do \
	  cp -f $$I.txt $(TDSDIR)/doc/$(PACKAGEROOT)/ ; \
	  mv $(TDSDIR)/doc/$(PACKAGEROOT)/$$I.txt $(TDSDIR)/doc/$(PACKAGEROOT)/$$I ; \
	done
	cd $(TDSDIR) ; \
	zip -ll -q -r -X $(PACKAGE).tds.zip .
	cp $(TDSDIR)/$(PACKAGE).tds.zip ./
	rm -rf $(TDSDIR)

unpack:
	echo "Unpacking files"
	for I in $(UNPACK) ; do \
	  tex $$I &amp;&gt; /dev/null ; \
	done
```

You'll see that on Unix (where we have more tools definitely available) some things are easier. That also applies to finding the local tex root: TeX Live will almost certainly be the TeX system installed, so its tools can be called on to collect the data needed. Both of the above should work with the demonstration package code I talked about last week.
