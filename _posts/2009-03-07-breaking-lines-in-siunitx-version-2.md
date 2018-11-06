---
id: 219
title: Breaking lines in siunitx version 2
date: 2009-03-07T16:46:47+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=219
permalink: /2009/03/07/breaking-lines-in-siunitx-version-2/
categories:
  - Packages
  - siunitx
---
Line breaks between units and values are frowned upon by those “in the know”, as the unit–value combination is mathematically one entity. Despite that, in reality this is a feature I've been asked for in [siunitx](http://www.ctan.org/pkg/siunitx).The way I'm implementing things, this is not technically difficult to implement. With a suitable warning, I will include the ability to break between units and values in siunitx version 2.

The other place you could place breaks is between different units (assuming a space is being used as the unit separator). This is much more problematic for a number of reasons. First, unlike between numbers and units, the inter-unit separator might be one of various things. The space between a value and a unit is always some kind of white space, and is always expected by the reader. So working out if a break is sensible would not be easy. Second, siunitx needs to handle two types of unit input, units as macros and literal input. I've steered away from processing literal units for various reasons, and reliably breaking both types of input looks difficult. Third, there is a technical problem. Simplifying how siunitx works, currently units are actually printed by some code that does:

<!-- {% raw %} -->
```latex
\hbox{%
  % Some font set up work for maths mode
  \ensuremath{%
    \mathrm{%
      unit \, unit \, unit
    }%
  }%
}
```
<!-- {% endraw %} -->

when printing in maths mode (the default). The key point is that everything needs to be inside an `\hbox` so that the formatting of maths can be influenced correctly. So breaking units here is not possible. To get around this, I'd need to print each unit separately, with the spaces outside the box.  This looks slow and unreliable. All things considered, I'm minded to keep the current approach to units: the unit is a non-divisible block.
