---
title: Uncertainties in siunitx
layout: post
permalink: /2023/08/2/uncertainties-in-siunitx
categories:
  - siunitx
---

Right from the first version, `siunitx` has supported uncertainty values in
numbers. Uncertainties are a key piece of information about a lot of scientific
values, and so it's important to have a convenient way to present them.

The most common uncertainty we see is one that is symmetrical, a value
plus-or-minus some number, for example 1.23 ± 0.04. This could be a standard
deviation from repeated measurement, or a tolerance, or derived some other way.
Luckily for me, the _source_ of such a value doesn't matter: `siunitx` just
needs to be able to read the input, store it and print the output. For both
reading and printing, `siunitx` has two ways of handling these symmetrical
uncertainties

- A 'long' form, in which the uncertainty is given as a complete number, for
  example 1.23 ± 0.04
- A 'compact' form, in which the uncertainly is shown relative to the digits in
  the main value, for example 1.23(4)

In version 3 of `siunitx`, I took that existing support and added a
long-requested new feature: rounding to an uncertainty. That means that if you
have something like 1.2345 ± 0.0367 and ask to round to one place, the
uncertainty is first rounded (to 0.04), then the main value is rounded to the
same precision (to 1.23).

Building on that, v3.1 added the idea of multiple uncertainties. These come up
in some areas (astronomy is one, particle physics another) where there are clear
sources of distinct uncertainty elements. Supporting multiple uncertainties also
means supporting _descriptions_ for them: if you are dividing up uncertainty,
you likely want to say why. So in v3.1, you can say `1.23(4)(5)` or `1.23 ± 0.04
± 0.05`, and set up the descriptors, and have something like `1.23 ± 0.04 (sys)
± 0.05 (stat)` get printed. I've not had any feedback yet on this new feature:
fingers-crossed that means it all works 100%!

Now, for v3.3, I've looked at another long-standing request: asymmetric
uncertainties. For this release, I've kept this are simple, as it's one I know
less about. There's just a 'compact' input form, and one (compact) output form.
So we can input `1.23(4:5)` and get in TeX terms `$1.23^{+0.04}_{-0.05}$`
typeset. Asymmetric and symmetric uncertainties can be intermixed, and you can
have multiple asymmetric ones. I'm hoping this feature gets picked up by users,
and that I get some idea of what to do next. I suspect there might be
alternative output formats requested, and I wonder whether a 'long' input form
`1.23 + 0.04 - 0.05` will be asked for: I've not done that yet as it's more
tricky if the user misses one part out!

Hopefully, with the introduction of asymmetric uncertainty support, `siunitx`
covers just about all types of uncertainty in scientific data: aiming to be a
_comprehensive_ (SI) units package, after all!