---
title: The good, the bad and the ugly: creating document commands
layout: post
permalink: /2020/08/19/the-good-the-bad-and-the-ugly-creating-document-commands
categories:
  - LaTeX3
tags:
  - xparse
  - document-commands
---

Creating document commands in LaTeX has traditionally involved a mix of
`\newcommand`, semi-internal kernel commands (like `\@ifnextchar` and
`\@ifstar`) and low-level TeX programming using `\def`. As part of wider
efforts to improve LaTeX, the team have over the past few years improved
[`xparse`](https://ctan.org/pkg/xparse) to the point where it is capable
of creating a vast array of document commands.

The aims of `xparse` have always been two-fold: to provide a clear way to
create _new_ commands, and to provide a language to describe _existing_ ones.
It is also intended to be as flexible as possible, so it doesn't impose
artificial restrictions on syntax. That comes at a cost, however: it can be
(ab)used to create commands that really don't fit into the standard LaTeX
pattern.

The upcoming LaTeX kernel release (autumn 2020) will integrate most, though
not all, of `xparse` into the kernel. That means the core ideas will be
available out-of-the-box. This seems like a good time, therefore, to look
at the best ways to use the abilities of `xparse` in making document
commands. I won't look at the full detail, rather pick out how to, and how not
to, create good document commands. (I'm going to assume some familiarity with
the `xparse` description syntax.)

## The Good

The LaTeX kernel is very careful to have consistent syntax for document
commands. It uses a very small number of argument types, which I'll describe
in `xparse` terms

- Mandatory (`m`) arguments in braces
- Optional (`o`/`O{<defaut>}`) arguments in `[]`, which may have a default; in
  `xparse` terms we can tell the difference between a missing optional argument
  and one given with an empty `[]` pair
- A star (`s`)
- Picture co-ordinates (`r()`), which are split into _x_ and _y_, so in
  `xparse` terms subject to `\SplitArgument`

Mot of the time, the LaTeX kernel makes arguments _long_, which is shown as
`+` in `xparse` syntax.

A star is _always_ used as the first argument after a command, so in some ways
it looks like part of the command name itself. Optional arguments are _almost_
always given before mandatory ones, and most of the time there is _only one_.
Where two are used, for example with `\makebox`, it's because the second is
_strictly dependent_ on the presence of the first.

Following the kernel, signatures (argument descriptions) such as `s o m`,
`s O{<default>} m m` and `o m m` are 'good'. You _can_ use something like
`s +m O{0} +o +m` (the syntax of `\newcommand`!) if you are careful, but
_think very carefully_.

There's one syntax that's not from the kernel but is recommended where it
applies: [`beamer`'s'](https://ctan.org/pkg/beamer) overlay syntax, which is
`d<>` in `xparse` terms. This always comes first (other than a star), and is
best reserved for the 'on X slides of Y' idea in presentations (doesn't have
to be using `beamer`).

`xparse` lets us create arguments using `_` and `^`, similar to TeX's core
math mode syntax. Most of the time, this should be reserved for math mode
where you need to emulate the TeX syntax but need for some reason to grab
the arguments yourself. That's done using `e{^_}`: I'd restrict this to
math mode commands.

## The Bad

The above already shows we have quite a few combinations available. Things go
bad when too many combinations are used. That includes things like

- Multiple optional arguments where the second or subsequent ones don't
  strictly depend on the earlier ones
- Optional arguments using tokens other than `[]` (or `<>` for overlays)
- Testing for tokens other than `*` as 'a special case' (think things like `+`)

Almost always, complex set ups using these types of combination mean _you need
to rethink the syntax_. In particular, multiple optional arguments tend to
be much better replaced by using a keyval approach.

## The Ugly

Some ideas in `xparse` won't be making it to the kernel: these are definitely
the Ugly. They'll stay in a stub `xparse` for historical reasons, and as they
do describe some syntax choices people have made, but really they should be
avoided

- _Optional_ groups (`g`) in braces; breaks the LaTeX conventions badly
- Arguments _up to_ a left brace (`l`); useful at a low level, but not in
  a document command
- Arguments _up to_ a token (`u`); widely used in programming, but again not
  in document commands

You might wonder why they are all there in the first place: these were part of
the more experimental work in `xparse`, and those particular experiments have
shown we don't want to enable such syntaxes even for emulating existing
commands.

## A Fistful of Tokens

There are of course places where you need to go outside of the `xparse`
structures, particularly when parsing specialist data. The popular TikZ
graphics system is one example, linguistic glosses are another. But these
are always restricted contexts: normally within a dedicated environment where
it is clear that the 'usual' rules do not apply. Basically, if you do this,
you are on your own, so be sure to check the balance of consistency _versus_
compactness.

## For a Few Tokens More

Using `xparse` syntax makes it _much_ easier to have a clear break between
interface and implementation. As such, the fact that it's go more going on
'beneath the hood' is worth it: it's a lot easier to track what's happening.
The move into the kernel will make using `xparse` descriptions even easier to
exploit, so it's important users give a little thought to the syntax they
choose. 
