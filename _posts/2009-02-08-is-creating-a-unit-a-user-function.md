---
title: Is creating a unit a 'user' function?
layout: post
permalink: /2009/02/08/is-creating-a-unit-a-user-function/
categories:
  - Packages
  - siunitx
---
Working on `siunitx` version 2, I'm confronted with a slight problem.  Currently, the macros used to manipulate units are called

- `\newunit`
- `\renewunit`
- `\provideunit`

which follows the LaTeX 2e `\newcommand`, _etc._; the same is true for prefixes and so forth.  These names were probably not the best choice: for example, [`biblatex`](https://ctan.org/pkg/biblatex) also has a `\newunit` macro (although there is not a clash, luckily).

I've been thinking of better names, but I'm not sure whether these should be document level (all lower-case), or design level (mixed upper-case and lower-case). Some ideas:

1. `\DeclarePhysicalUnit` (create without checks)
2. `\NewPhysicalUnit` (create with checks: would require `\RenewPhysicalUnit`, _etc._)
3. `\NewUnit` (as 2 but shorter)
4. `\newphysicalunit` (as 2 but document level)
5. `\createphysicalunit` (is 'create' better than 'new'?)
6. `\createunit` (avoids the confusion with `biblatex`)

You'll see that I've not included 'SI' in any of the above: it looks odd, and of course you can create non-SI units anyway.  How do other people see this?
