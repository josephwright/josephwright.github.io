---
title: Units in ConTeXt
layout: post
permalink: /2009/01/16/units-in-context/
categories:
  - Packages
  - siunitx
tags:
  - ConTeXt
  - units
---
Looking to gather ideas, I was looking at the [ConTeXt](http://wiki.contextgarden.net) '[units](http://wiki.contextgarden.net/Units)' module. The approach taken there is to create free-standing macros, such as `\Second` or `\Candela`, and to use them to build up a string of units. Like some of the LaTeX solutions, this means that the user has to manually include symbols (such as `\Times`) to get the formatting right. On the other hand, ConTeXt uses a glossary-like method for defining units (something I've thought about for [`siunitx`](https://ctan.org/pkg/siunitx) in the past).  I'll certainly be thinking about something like that for `siunitx` version 2.
