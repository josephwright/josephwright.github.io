---
id: 909
title: Using \let to remove a space
date: 2011-02-05T07:39:27+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=909
permalink: /2011/02/05/using-let-to-remove-a-space/
categories:
  - General
---
On the [{TeX} Q&amp;A site](https://tex.stackexchange.com/), there was a question recently about [splitting the first token off a list](https://tex.stackexchange.com/questions/10210/), with the requirement that spaces are not skipped. In my answer, I've used \let to remove one space. The question is how to do this. Normally, if you want to use `\let` you do

```latex
\let\TokenA\TokenB
```

In this case, TeX will skip spaces after `\let` and `\TokenA`, so we can't use it to `\let` to a space. However, what we can do is notice that TeX allows us to have an optional `=` followed by one space in the syntax for `\let`. We also need to make sure that TeX does not discard two spaces in the early stage of parsing, so can use `\@firstonone`:

```latex
\@firstofone{\let\TokenA= }
```

This will `\let` `\TokenA` to the next token in the input, even if it is a space. I've used this to remove the next token from some input in combination with `\afterassignment`:

<!-- {% raw %} -->
```latex
\long\def\firstofone#1{#1}
\def\GobbleExactlyOne{%
  \afterassignment\NextThing
  \firstofone{\let\TokenA= }%
}
```
<!-- {% endraw %} -->

Not something you need every day, but worth knowing about I think.
