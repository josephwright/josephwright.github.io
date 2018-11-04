---
id: 273
title: achemso updated to version 3.2
date: 2009-04-21T07:39:25+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=273
permalink: /2009/04/21/achemso-updated-to-version-32/
categories:
  - achemso
  - Packages
---
I've just uploaded version 3.2 of <a title=" 	Support for American Chemical Society journal submissions." href="http://www.ctan.org/pkg/achemso">achemso</a> to <a title="The Comprehensive TeX Archive Network" href="http://www.ctan.org">CTAN</a>, and also sent it off the the <a title="American Chemical Society" href="http://www.acs.org">American Chemical Society</a>. The development for v3.2 has mainly been about making using the package easier for end users. I've removed a lot of dependency on other support packages, so that it only uses very standard LaTeX packages (things like <a title="Improved interface for floating objects" href="http://www.ctan.org/pkg/float">float </a>and <a title="Customising captions in floating environments" href="http://www.ctan.org/pkg/caption">caption</a>). I've also made the package cope better with older versions of <a title="Extension of the keyval package" href="http://www.ctan.org/pkg/xkeyval">xkeyval</a>, by using only a subset of the functions provided there. There are a few bug fixes as well, plus a new environment for graphic TOC entries. Hopefully, this makes life easier for manuscript authors.