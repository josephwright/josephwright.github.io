---
title: \NewDocumentCommand versus \newcommand versus ...
layout: post
permalink: /2020/08/20/newdocumentcommand-versus-newcommand-versus
categories:
  - LaTeX3
tags:
  - xparse
  - document-commands
---

Creating new document commands in LaTeX has traditionally been the job of
`\newcommand`. This lets you create command with mandatory arguments, and can
also add a first optional argument. However, it can't create more complex
commands: LaTeX uses for examples stars, multiple optional arguments, _etc._ To
create these, the kernel itself uses lower-level TeX programming. But this is
opaque to many users, and a variety of packages have been created to ease the
burden.

Over the last decade, the LaTeX team have developed
[`xparse`](https://ctan.org/pkg/xparse), a generic document command parser, as a
way to unify many ideas and provide a single consistent way to create document
commands. Most of that code will soon be moving to the LaTeX kernel itself, and
I've [provided some
ideas](2020-08-19-the-good-the-bad-and-the-ugly-creating-document-commands)
about how best to exploit that in a recent post..

Here, I want to look at a related issue: why use the `xparse` approach, and how
it compares to existing solutions, both in the LaTeX kernel and the wider
package sphere. Here, I'm going to avoid talking about 'simple' shortcuts
(things like `\newcommand\myname{Joseph Wright}`): these are best left to
`\newcommand`. Instead, I want to deal with commands which take arguments and
have some element of 'programming' to them.

What I'll seek to highlight here is that using `\NewDocumentCommand`, we get
a single consistent and reliable way to create a variety of commands. There's
no need to worry about clashes between approaches, and it all 'just works'.

## Preliminaries: protected commands and optional arguments

Before we start, a couple of things are worth mentioning. First, there is the
idea of 'protected' commands. In some places, we need commands not to 'expand'
(turn into their definition). With a modern TeX system, that can be arranged by
the engine itself (pdfTeX or similar), using 'e-TeX' and the `\protected`
primitive (built-in). The LaTeX kernel doesn't use that mechanism in
`\newcommand`, but lots of other tools do. I'm going to assume that we want to
make protected commands unless I mention otherwise. Almost always, unless you
are creating a 'shortcut' for some text, you want your commands to be protected.

The second thing to note is that TeX itself has no concept of optional
arguments, so they are arranged using some clever look-ahead code. In `xparse`,
nested optional arguments are handled automatically, but again, `\newcommand`
and similar do not do that.

## The kernel: _versus_ `\newcommand`

The kernel's `\newcommand` can, as I've said, create commands with multiple
mandatory arguments but only with one optional one. As a simple example, we
might have
```latex
\newcommand\foo[3][default]{%
    Code perhaps using #1 and definitely using #2 and #3%
}
```

We can of course do the same using `\NewDocoumentCommand`
```latex
\NewDocoumentCommand\foo{+O{default} +m +m}{%
    Code perhaps using #1 and definitely using #2 and #3%
}
```
You'll notice that I've use `+m` for the mandatory arguments, as that matches
`\newcommand`: the arguments can accept paragraphs. With `\newcommand`, all
arguments either accept `\par` or do not: with `\NewDocumentCommand` we can
select on a per-argument level what happens.

Th optional argument with a default works using `O{default}`, and the result
will be the same functionality. We gain the idea that nested optional arguments
are parsed properly, some better error messages if we use `\foo` incorrectly,
and an engine-robust definition of `\foo`.

We can't do a lot more with `\newcommand`, so rather than try to show off other
`\NewDocumentCommand` features here, we'll first consider how we might make more
complex syntaxes using just the classical LaTeX kernel.

## The kernel: _versus_ `\def`

Using the TeX primitive `\def`, plus the kernel internal commands `\@ifstar` and
`\@ifnextchar`, we can construct more complex syntaxes. For example, let's
create the syntax for `\section`: a star, and optional argument and a mandatory
one. I'll assume we are have `@` as a letter here. I'm also going to pass the
presence of a star as the text `true` or `false`, as it makes things clearer.

```latex
\newcommand\section{%
    \@ifstar
      {\section@auxi{true}}
      {\section@auxi{false}}%
}
\def\section@starred#1{%
    \@ifnextchar[%]
      {\section@auxii{#1}}
      {\section@auxii{#1}[]}%
}
\long\def\section@auxii#1[#2]#3{%
    % Here:
    % #1 is "true"/"false" for a star
    % #2 is the optional argument
    % #3 is the mandatory argument
}
```

As you'll see, this is a bit tricky already, and it doesn't cover the case where
we want to have the optional argument default to the mandatory one, when it's
not given. It also doesn't allow for nested optional arguments, and it's not
engine-robust. We might of course use more complex paths for the star: we could
have independent routes.

Using `\NewDocumentCommand`, things are a lot easier
```latex
\NewDocoumentCommand\section{s +O{#3} +m}{%
  % Here:
  % #1 is "true"/"false" for a star
  % #2 is the optional argument
  % #3 is the mandatory argument
}
```
The minor difference now is that `#1` is a special token that we can test for
truth using `IFBooleanTF`. I've also allowed for the optional argument picking
up the mandatory one, when it's not given.

We could make more complex examples, but the bottom line remains the same:
using `\NewDocumentCommand`, we are always going to have simple one-line
interface descriptions, and the behind-the-scenes TeX argument parsing
is all hidden away.

## `etoolbox`: _versus_ `\newrobustcmd`

The [`etoolbox`](https://ctan.org/pkg/etoolbox) package offers `\newrobustcmd`
as a complement to `\newcommand`. It does _exactly the same_ as `\newcommand`,
except it uses e-TeX to make engine-protected commands. So from an interface
point-of-view, there's nothing new here.

## `twoopt`: _versus_ `\newcommandtwoopt`

The [`twoopt`](https://ctan.org/pkg/twoopt) package allows a syntax similar to
`\newcommand` but for creating two optional arguments. We'll take an example
from it's documentation:
```latex
\newcommandtwoopt\bsp[3][AA][BB]{%
    \typeout{\string\bsp: #1,#2,#3}%
}
```
This is reasonably clear: we have an optional argument `#1`, and optional
argument `#2` and a mandatory argument `#3`. The two optional arguments each here
have a default.

How does that look with `\NewDocumentCommand`?
```latex
\NewDocumentCommand\bsp{+O{AA} +O{BB} +m}
    \typeout{\string\bsp: #1,#2,#3}%
}
```
You'll see that we stay consistent here: the same syntax is used to create one,
two or even more optional arguments. I wouldn't recommend using multiple
optional arguments in most case, but when we do, it's a lot easier using
`\NewDocumentCommand`.

What `twoopt` _cannot_ do, but `\NewDocumentCommand` can, is create optional
arguments that are not in the first/second positions. That would require either
the TeX coding we've already seen, or using a different tool again, if we were
using `twoopt`.

## `suffix`: _versus_ `\withsuffix`

The [`suffix`](https://ctan.org/pkg/suffix) package allows one to extend an
existing command to look for an optional token ('suffix') immediately after the
command name. Taking a simple example [from
StackExchange](https://tex.stackexchange.com/a/4388/73), we start with
```latex
\newcommand\foo{blah}
\WithSuffix\newcommand\foo*{blahblah}
```
which translates to
```latex
\NewDocumentCommand\foo{s}{%
   \IFBooleanTF{#1}
     {blah}
     {blahblah}
}
```

This means we only need one line for the interface set up, and don't need for
example to split up grabbing optional arguments into two different places
(back for example with `\section`).

## `xargs`: _versus_ `\newcommandx`

The [`xargs`](https://ctan.org/pkg/xargs) package is perhaps the most complete
approach to extending `\newcommand` as far as optional arguments are concerned.
It introduces `\newcommandx`, which has the same syntax as `\newcommand` but
where the second optional argument is a keyval list. That then described which
arguments are optional, and what their defaults are. Taking an example from the
documentation
```latex
\newcommandx*\coord[3][2=1,3=n]{(#2_{#1},\ldots,#2_{#3})}
```
would create a command with two optional arguments, `#2` and `#3`, leaving `#1`
mandatory. Translating into `\NewDocumentCommand` syntax might make that
clearer!
```latex
\NewDocumentCommand\coord{m O{1} O{n}}{%
    (#2_{#1},\ldots,#2_{#3})%
}
```

`xargs` has the idea of `usedefault`, which allows `[]` to be the same as
`[default]`. That's not something `xparse` does, as it is pretty confusing: what
happens when you want an empty optional argument? This links to something I've
said before: avoid consecutive optional arguments _unless_ the second is
dependent on the first.

## `newcommand`: _versus_ `newcommand.py`

Stepping outside for TeX itself, Scott Pakin's
[`newcommand.py`](https://ctan.org/pkg/newcommand) Python script provides a
description language somewhat like `xparse`, and converts this into a 'template'
of TeX code, allowing a 'fill in the blanks' approach to creating commands. It
can cover several of the ideas that `xparse` can, including a few that will
_not_ be migrated to the LaTeX kernel. It can also set up a command taking more
than 9 arguments, but that's always going to be tricky as a user.

What is important is that using a script means we have to work in two
steps, and it's hard to see what's happening from the TeX source. It also
doesn't offer anything that the kernel doesn't already do: no protected
commands, no nested optional arguments, no improved error messages. So in
many ways this is simply techniques we've already seen, just made a little
more accessible, at least if you have Python installed.

## `environ`: _versus_ `\NewEnviron`

As well as document _commands_, the `xparse` syntax can be used to create
document environments: the same relationship we have between `\newcommand`
and `\newenvironment`. What people sometimes want to do is grab an entire
document environment body and use it like a command argument. Classically,
one does that using the [`environ`](https://ctan.org/pkg/environ)
package. Again, taking an example from the documentation
```latex
\NewEnviron{test}{%
  \fbox{\parbox{1.5cm}{\BODY}}\color{red}
  \fbox{\parbox{1.5cm}{\BODY}}%
}
```
would grab all of the body of the environment `test` and set it twice: the
body is saved a `\BODY`.

Using `\NewDocumentEnvironment`, we have a syntax similar to `\newenvironment`
```latex
\NewDocumentEnvironment{test}{+b}{%
  \fbox{\parbox{1.5cm}{#1}}\color{red}
  \fbox{\parbox{1.5cm}{#1}}%
}{}
```
with the argument grabbed in the normal way as (here) `#1`. We can therefore
have 'real' arguments first, then grab the body.

## Summary

Using the tools set up in `\NewDocumentCommand`, we can have a consistent
way of creating a wide range of document commands. Rather than use a mixture
of tools, from the kernel, TeX itself and the package sphere, it is far
preferable to use the single interface of `\NewDocumentCommand` for all
commands today.
