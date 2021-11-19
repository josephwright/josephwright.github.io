---
title: "xparse: optional arguments (at the end)"
layout: post
permalink: /2018/04/21/xparse-optional-arguments-at-the-end/
categories:
  - General
tags:
  - LaTeX3
  - xparse
---
For many years, the LaTeX team have been wondering about a subtle question: how do we deal with spaces before optional arguments. It's easy enough if we know there are more mandatory arguments to look for:

```latex
\foo{first}  [optional]  {second}
```

should be treated in the same way as

```latex
\foo{first}[optional]{second}
```

However, when the optional argument comes last, it's a bit more tricky. It's easy enough to have

```latex
\foo{first}[optional]
\foo{first}  [optional]
```

both do the same thing, but there is one classic LaTeX2e case to worry about. When you load `amsmath`, you'll find that

```latex
\begin{align}
   a  & b \\
  [c] & d \\
\end{align}
```

doesn't treat `[c]` as the optional argument to `\\`: spaces are _not_ skipped here. (This is pretty sensible for mathematics: it's quite possible to have something in square brackets.)

To date, we've handled this by simply not allowing any spaces before optional arguments when they come 'at the end' (after any mandatory ones). However, that means it applies to all cases, which we've thought for some time was not ideal: most of the time, spaces here are likely fine.

For the next release of `xparse`, we've revisited this area and introduced a new `!` modifier for optional arguments. Unmodified optional arguments will now allow spaces, with the `!` modifier preventing this. Thus we can now describe `\\` as having `xparse` set up

```latex
\DeclareDocumentCommand{\\}{!s !o}{<code>}
```

meaning no spaces are allowed, whilst most other commands will now allow spaces. This should affect very few *end user* documents, but does make for a better long-term approach.
