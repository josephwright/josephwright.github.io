---
title: When to use \protected
layout: post
permalink: /2010/10/07/when-to-use-protected/
categories:
  - General
tags:
  - etex
  - protected
  - robust
---
e-TeX introduced the idea of 'protected' macros over ten years ago, but many experienced (La)TeX users struggle with the concept. The idea of the `\protected` primitive is that it will prevent a macro being expanded inside an `\edef` or `\write`, so that

```latex
\protected\def\example{Hello}
\edef\test{\example}
\show\test
```

will give

```latex
\test=macro:
->\example .
```

Why would you want to do this? Well, there are some things that do not work properly inside an `\edef`. The classic one is an assignment: the following does not work

```latex
\edef\fails{\def\fails{stuff}}
```

This will give an undefined control sequence error for `\fails`, rather than carrying out in 'inner' `\def`. So as part of a general strategy I would recommend always making any macro that performs an assignment protected. That also applies if you know that one macro will use another that is itself protected. This is exactly what we've been doing in the work on [LaTeX3](https://www.latex-project.org/latex3.html), where the aim is that all macros are either protected or will expand safely inside an `\edef`. However, the idea applies more widely: making things protected is a lot more reliable than using LaTeX's 'robust' mechanism, and avoids some nasty errors. e-TeX has been around long enough that there is no real excuse not to make use of this mechanism.
