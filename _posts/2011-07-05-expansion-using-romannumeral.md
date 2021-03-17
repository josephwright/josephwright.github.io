---
title: Expansion using \romannumeral
layout: post
permalink: /2011/07/05/expansion-using-romannumeral/
categories:
  - General
---
There was [recent question on TeX.SX about expansion](https://tex.stackexchange.com/q/22288/73), where I suggested using `\romannumeral` for full expansion. This idea comes up quite often, so I thought it would be useful to look at how it works.

The `\romannumeral` primitive was intended to turn integers into roman numerals. As such, the input to `\romannumeral` should be an integer, in the same way that the input to `\number` is an integer. However, while `\number` produces output for both positive and negative integer input, `\romannumeral` produces no output at all for valid negative integer input. That is pretty clear with a simple case such as

```latex
\romannumeral -15
```

but becomes more powerful when used along with the `` ` `` syntax which TeX allows for including an integer

```latex
\romannumeral -`0
```

Here, the `` `0 `` is converted into a integer which TeX treats as complete: `` `0 `` is 48, but `` `01 `` is the (terminated) integer 48 followed by a separate 1 and _not_ the integer 481. The important thing for expansion, however, is that TeX always looks for an optional space to gobble after an integer, even in a case like `` `0 `` where the integer is automatically terminated.

How does this help with expansion? It's all to do with how TeX terminate numbers. If we have the demonstration macro

<!-- {% raw %} -->
```latex
\def\demo#1{%
  \detokenize\expandafter{\romannumeral-`0#1}%
}
```
<!-- {% endraw %} -->

the `\romannumeral` will produce no output (as the number it finds is &minus;48). However, it will expand `#1` until it finds an unexpandable token. That means that something like

```latex
\def\testa{\testb}
\def\testb{\testc}
\def\testc{abc}
\demo{\testa}
```

will be expanded to `abc` without needing to know in advance how many expansions are needed. In a real case, this is a great way to fully-expand `\if...` tests and so on, leaving only the result, but without needing to know how many expansions are needed (and having long `\expandafter` runs).

What you should notice here is that TeX will reinsert the expanded result, and will not complain if something non-expandable appears

```latex
\def\testa{\relax}
\demo{\testa}
```

will print `\relax`, as this is inserted with no errors or loss of unexpandable tokens.

The only proviso here is that TeX stops at the first non-expandable item. So something like

```latex
\def\testa{ \testb}
\def\testb{123}
\demo{\testa}
```

will stop at the space in `\testa` and not expand `\testb`. For real applications, that is not usually an issue as we are usually aiming to expand the beginning of the input.
