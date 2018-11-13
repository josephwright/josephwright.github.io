---
title: LuaTeX&#58; Manipulating UTF-8 text using Lua
layout: post
permalink: /2014/07/08/luatex-manipulating-utf-8-text-using-lua/
categories:
  - General
tags:
  - Lua
  - LuaTeX
  - Unicode
  - UTF-8
---
Both the XeTeX and LuaTeX engines are natively UTF-8, which makes input of non-ASCII text a lot easier than with pdfTeX (certainly for the programmer: `inputenc` hides a lot of complexity for the end user!). With LuaTeX, there is the potential to script in Lua as well as program in TeX macros, and that of course means that you might well want to do manipulation of that UTF-8 input in Lua. What might then catch you out is that it's not quite as simple as all that!

Lua itself can pass around arbitrary bytes, so input in UTF-8 won't get mangled. However, the basic string functions provided by Lua are _not_ UTF-8 aware. The LuaTeX manual cautions

> The `string` library functions `len`, `lower`, `sub`, etc. are not UNICODE-aware.

As a result, applying these functions to anything outside the ASCII range is not a good idea. At best you might get unexpected output, so

```lua
tex.print (string.lower ("Ł"))
```

simply prints in `Ł` (with the right font set up). Worse, get an error as for example

```lua
tex.print (string.match ("Ł","[Ł]"))
```

results in

```
! String contains an invalid utf-8 sequence.
```

which is not what you want!

Instead of using the `string` library, the current correct approach here is to use `slnunicode`. Again, the LuaTeX manual has some advice:

> For strings in the UTF-8 encoding, i.e., strings containing characters above code point 127, the corresponding functions from the `slnunicode` library can be used, e.g., `unicode.utf8.len`, `unicode.utf8.lower`, etc.

and indeed

```lua
tex.print(unicode.utf8.lower("Ł"))
```

does indeed print `ł`. There are still a few things to watch, though. The LuaTeX manual warns that `unicode.utf8.find` returns a byte range and that `unicode.utf8.match` and `unicode.utf8.gmatch` fall back on non-Unicode behaviour when an empty capture (`()`) is used. Both of those can be be allowed for, of course: they should not be big issues.

There's still a bit of complexity for two reasons. First, there's not really much documentation on the `slnunicode` library, so beyond trying examples it's not so easy to know what 'should' happen. For example, case-changing in Unicode is more complex than a simple one-to-one mapping, and can have language-dependencies. I'll probably return to that in another post for a TeX (or at least XeTeX/LuaTeX) take on this, but in the Lua context the problem is it's not so clear quite what's available! In a way, the second point links to this: the LuaTeX manual tells us

>  The `slnunicode` library will be replaced by an internal UNICODE library in a future LuaTeX version.

which of course should lead to better documentation but at the price of having to keep an eye on the situation.

Over all, provided you are aware that you have to think, using Lua with Unicode works well, it's just that it's not quite as obvious as you might expect!
