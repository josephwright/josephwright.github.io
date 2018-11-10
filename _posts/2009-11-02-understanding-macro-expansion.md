---
title: Understanding macro expansion
layout: post
permalink: /2009/11/02/understanding-macro-expansion/
categories:
  - General
---
I get the occasional e-mail asking me to explain who some complex macro works. I usually answer by trying to show how I go about understanding things. There are a few simple steps:

1. Start from the definition of the first macro you want to understand.
2. From the definition, work out what arguments it will take (easy if they are not delimited).
3. Replace every parameter in the definition by what you picked up in (2). Don't worry if things seem like they will change part way through: TeX has to fill in every `#1`, `#2`, _etc_. at the point of expansion.
4. Now work through the expansion systematically. If you come to another macro, replace it by it's expansion (remembering any arguments), if you hit a primitive, work out what it will do, _etc_.
5. It's important not to get confused by things that are redefined themselves during the expansion. TeX uses whatever the current meaning is when it expands/executes a token. So it's often useful to keep notes on definitions, _etc_., and check against them.

Usually, with a bit of care and some notes, enlightenment will dawn.
