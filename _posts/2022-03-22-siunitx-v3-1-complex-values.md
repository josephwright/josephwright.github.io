---
title: "siunitx v3.1: complex values"
layout: post
permalink: /2022/03/22/siunitx-v3-1-complex-values
categories:
  - siunitx
---

I mentioned [recently](/2022/03/11/siunitx-v3-1-development) that I'm working on
features for [`siunitx`](https://ctan.org/pkg/siunitx) v3.1. One area that I've
now been able  to commit is improvements to handling complex values.

In v2, you could give complex values in the normal argument to `\num` or `\SI`.
I removed that for v3, and of course that was not entirely popular. Instead, I
introduced dedicated commands, `\complexnum` and `\complexqty`. Part of the
reason  for that was that it makes the implementation of `\num` and `\qty`/`\SI`
easier. But the other was that I wanted to address polar form, and that really
didn't  look viable if it was mixed in with the normal numerical argument type.

I've now [committed a
change](https://github.com/josephwright/siunitx/commit/782e8f0a8a2d08592870023a7584c8735775f96f)
that introduces support for polar form in `siunitx`. So what happens now is if
you give a value such as `\num{10:30}`, it's treated as a magnitude and an
angle. The latter has a setting to determine if it's regarded as being in
degrees or radians. The package can then typeset the result in a similar form,
using the `\angle` symbol between the two parts. You can also set up to  convert
between the classical (Cartesian) and polar forms of the value. So hopefully
this shows why I wanted to separate out complex numbers: they need special
handling, and now they get it.
