---
title: Choice options
layout: post
permalink: /2008/12/28/choice-options/
categories:
  - Packages
  - siunitx
---
As I work through recoding `siunitx` for version 2, I'm re-thinking all of the options. As I've said already (and others have said too) the current structure is too complex. A particular problem is the options which currently take a choice of values, or a literal item.  I'm thinking that it would be better to either (a) have a fixed list of choices or (b) use the input as given. For example, the current:

```latex
\sisetup{decimalsymbol = comma}
```

could become either:

```latex
\sisetup{numbers/output/decimal marker = comma}
```

or

```latex
\sisetup{numbers/output/decimal marker = {,}}
```

For options which give literal output (like the above), I think the later method is better (it matches up with the input options, for example). On the other hand, some options (particularly those involving spaces) seem better done using keywords:

```latex
\sisetup{numbers/output/digit separator = thick space} % thin space, comma, ...
```

I'd be keen to see what others think.
