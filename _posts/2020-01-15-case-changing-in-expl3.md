---
title: Case changing in expl3
layout: post
permalink: /2020/01/15/case-changing-in-expl3
categories:
  - LaTeX3
tags:
  - Unicode
  - UTF-8
---

A [few years ago](/2014/07/10/case-changing-solving-the-challenges-in-tex/)
I wrote about the work the LaTeX team were doing on providing case changing
functions in `expl3`. Since then, the code has been tested and revised,
and very recently has moved to a 'final' home within `expl3`. It therefore
seems like a good time to look again at what the challenges are and what tools
we've provided.

It's worth noting up-front that all of the `expl3` functions work with UTF-8
input, and as far as possible case changing (and other text manipulation)
follows the [Unicode Consortium](https://www.unicode.org/) guidelines.

## Different kinds of input, different kinds of case changing

To understand what functions we've provided for case changing, we first have
to know what different types of input we might be dealing with. There are
broadly two types

- Text: material that we will want to typeset or similar, and which contains
  natural language content. This material might also have some formatting,
  and may be marked up as being in a particular language.
- Strings: material used in code, for example as identifiers, to construct
  control sequences or to find files. This material will never have formatting,
  and should always give the same outcome, irrespective of the language a
  document is written in.

Unsurprisingly, case-changing strings is a lot more straight-forward than
case-changing text. They 'live' in different parts of the `expl3` code, so
I'll look at them separately.

## Strings

In TeX terms, a string is a series of characters which are all treated as
'other' tokens (except spaces, which are still spaces). That's important
here because it means strings won't contain any control sequences, and because
with pdfTeX there can't be any (useful) accented characters.

The most obvious need to handle case in programming strings is when comparing
in a caseless manner: 'removing' the case. Programmers often do that by
lowercasing text, but there are places where that's not right. For example,
Greek has two forms of the lowercase sigma (&sigma; and &sigmaf;), and these
should be treated as the same for a caseless test. Unicode define the correct
operation: case _folding_. In `expl3`, that's called `\str_foldcase:n`.

```LaTeX
\exp_args:Ne \str_show:n
  { \str_foldcase:n { AbC } }
```

_Much_ more rare is the need to upper- or lowercase a string. Unicode do not
mention this at all, but in TeX we might want to construct a control sequence
dynamically. To do that, we might want to uppercase the first character of some
user input _string_, and lowercase the rest. We can do that by combining
`\str_uppercase:n` and  `\str_lowercase:n` with the `\str_head:n` and
`\str_tail:n` functions:

```LaTeX
\exp_args:Ne \str_show:n
  {
    \str_uppercase:f { \str_head:n { SomeThing } }
    \str_lowercase:f { \str_tail:n { SomeThing } }
  }
```

## Text

### The basics

Case changing text is much more complicated because it has to deal with control
sequences, accents, math mode and context. The first step of case changing
here is to expand the input as far as possible: that's done using a function
called `\text_expand:n` which works very similarity to the LaTeX2e command
`\protected@edef`, but is _expandable_. We don't really need to worry too much
about this: it's built in to the case changing system anyway.

Upper- and lowercasing is quite straight-forward: the functions have the
natural names `\text_uppercase:n` and `\text_lowercase:n`. These deal correctly
with things like the Greek final-sigma rule and (with LuaTeX and XeTeX) cover
the full Unicode range.

```LaTeX
% Try with XeTeX or LuaTeX
\exp_args:Ne \tl_show:n
  {
    \text_uppercase:n { Ragıp~Hulûsi~Özdem } ~
    \text_lowercase:n { ὈΔΥΣΣΕΎΣ }
  }
```

A variety of standard LaTeX accents and letter-like commands are set up
for correct case changing with no user intervention required.
```LaTeX
\exp_args:Ne \tl_show:n
  {
    \text_uppercase:n { \aa{}ngst\o{}m  ~ caf\'{e} }
  }
```

### Case changing exceptions

There are places that case changing should not apply, most obviously to math
mode material. There are a set of exceptions built-in to the case changer, and
that list can be extended: it's easy to add the equivalent of `\NoCaseChange`
from the [`textcase`](https://ctan.org/pkg/textcase) package.

```LaTeX
\tl_put_right:Nn \l_text_case_exclude_arg_tl
  { \NoCaseChange }
\exp_args:Ne \tl_show:n
  {
    \text_uppercase:n { Hello ~ $y = max + c$ } ~
    \text_lowercase:n { \NoCaseChange { iPhone } ~ iPhone }
  }
```

### Titlecasing

Commonly, people think about uppercasing the first character of some text
then lowercasing the rest, for example to use it at the start of a sentence.
Unicode describe this operation as titlecasing, as there are some situations
where the 'first character' is handled in a non-standard way. Perhaps the best
example is `IJ` in Dutch: it's treated as a single 'letter', so _both_ letters
have to be uppercase at the start of a sentence. (We'll come to
language-dependence in a second.)

Depending on the exact nature of the input, we might want to titlecase the
first 'character' then lowercase everything else, or we might want just to
titlecase the first 'character' and leave everything else unchanged. These
are called `\text_titlecase:n` and `\text_titlecase_first:n`, respectively.

```LaTeX
\exp_args:Ne \tl_show:n
  {
    \text_titlecase:n { some~text } ~
    \text_titlecase:n { SOME~TEXT } ~
    \text_titlecase_first:n { some~text } ~
    \text_titlecase_first:n { SOME~TEXT }
  }
```

As we are not simply grabbing the first token of the input, non-letters are
ignored and the first real text is case-changed.
```LaTeX
\exp_args:Ne \tl_show:n
  {
    \text_titlecase:n { 'some~text' }
  }
```

### Language-dependent functions

One important context for case changing text is the language the text is written
in: there are special considerations for Dutch, Lithuanian, Turkic languages
and Greek. That's all handled by using versions of the case-changing functions
that take a second argument: a
[BCP 47](https://en.wikipedia.org/wiki/IETF_language_tag) string which can
determine the path taken.
```LaTeX
\exp_args:Ne \tl_show:n
  {
    \text_uppercase:n { Ragıp~Hulûsi~Özdem } ~
    \text_uppercase:nn { tr } { Ragıp~Hulûsi~Özdem }
  }
\exp_args:Ne \tl_show:n
  {
    \text_uppercase:n { ὈΔΥΣΣΕΎΣ} ~
    \text_uppercase:nn { el } { ὈΔΥΣΣΕΎΣ }
  }
```

Over time, mechanisms to link this behaviour to `babel` will be developed.

## Conclusions

Case-changing functions in `expl3` are now mature and stable, and ready for
wider use. It's likely that they will be made available as document-level
commands in the medium term, but programmers can use them now to make
handling this important aspect of text manipulation easier.
