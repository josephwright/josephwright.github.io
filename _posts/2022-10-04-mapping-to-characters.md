---
title: Mapping to characters
layout: post
permalink: /2022/10/04/mapping-to-characters
categories:
  - General
---

It is quite natural to think that separating a word up into individual
characters is quite easy. It turns out that for the computer this isn't really
the case. If we look at a system understaning Unicode (like XeTeX or LuaTeX),
most of the time one 'character' is stored as one codepoint. A codepoint is a
single character entity for a Unicode programme. For example, if we take the
input `café`, it is made up of four codepoints:

1. U+0063 (LATIN SMALL LETTER C)
2. U+0061 (LATIN SMALL LETTER A)
3. U+0066 (LATIN SMALL LETTER F)
4. U+00E9 (LATIN SMALL LETTER E WITH ACUTE)

So we could in XeTeX/LuaTeX use a simple mapping to grab one character at a time
and do stuff with it. However, that's not always the case. Take for example
`Spın̈al Tap`. The dotless-i is a single codepoint, but there is not a codepoint
for an umluated-n. Instead, that is represented by two codepoints: a normal n
and a combining umlaut. As a user, it's clear that we'd want to get a single
'character' here. So there's clearly more work to do.

Luckily, this is not just a TeX problem and the Unicode Consortium have thought
about it for us. They provide a data file and rules that describe how to divide
input into _graphemes_: 'user perceived characters'.  So 'all' that is needed is
to examine the input using these rules, and to divide it up so that 'characters'
stay together.

For pdfTeX, there's an additional wrinkle: it uses bytes, not codepoints, and so
if we use a naïve TeX mapping, we would divide up any codepoing outside the
ASCII range into separate bytes: not good. Luckily, the nature of codepoints is
predictable: all that is needed is to examine the first byte and collect the
right number of further bytes to re-combine into a valid codepoint.

This work isn't something the average end user wants to do. Lcukily, they don't
have to as the LaTeX team have looked at this and created a suitable set of
`expl3` functions to do it: `\text_map_function:nN` and `\text_map_inline:nn`.
So for example we can do
```latex
\ExplSyntaxOn
\text_map_inline:nn { Spın̈al ~ Tap } { (#1) }
\ExplSyntaxOff
```
and get
```latex
(S)(p)(ı)(n̈)(a)(l)( )(T)(a)(p)
```
in any TeX engine (assuming we are set up to _print_ the characters, of course).
