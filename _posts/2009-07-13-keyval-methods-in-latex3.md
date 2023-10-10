---
title: Keyval methods in LaTeX3
layout: post
permalink: /2009/07/13/keyval-methods-in-latex3/
categories:
  - expl3
---
I've been working for a while on a method to provide a reasonably powerful method for creating keyval input for [LaTeX3](https://www.latex-project.org/latex3.html). This has been going under the working title '`keys3`', but yesterday I took the plunge and added the code to the LaTeX3 [development repository](https://www.latex-project.org/code.html). For the moment, this can only be accessed _via_ SVN, but if the rest of the team are happy with the idea, it will appear in the next snap shot that is sent to [CTAN](https://www.ctan.org).

The ideas in the new module (now called `l3keys`) have been inspired by the [`pgfkeys`](https://ctan.org/pkg/pgf) package. By using keyval methods to create keys, the idea is to make life a lot easier for the programmer. However, things are somewhat modified compared to the `pgfkeys` package, mainly to try to keep the input syntax simple but powerful enough for most uses. For example, there are separate functions for creating keys and setting them, an idea that all other keyval packages use. So a typical setup block might look like:

```latex
\keys_define:nn { module } {  
  key-one   .set:N     = \l_module_one_tl,   % Store input in variable
  key-one   .value_required:,
  key-two   .bool:N    = \l_module_two_bool, % Either true or false
  key-three .code:n    = { Code using an argument #1 },
  key-three .default:n = text
}
```

while keys are set using:

```latex
\keys_set:nn { module } {
  key-one = Value,
  key-two = true,
  key-three
}
```

Hopefully, the ideas are flexible and clear enough for people to get working with. One thing to notice: the key names are hyphenated. It looks like that will be the 'style guide' suggestion for LaTeX3 keys. At some point, I'll look at writing a [_TUGBoat_](https://tug.org/TUGboat/) article on how everything works.
