---
title: siunitx development: Notes for my future self
layout: post
permalink: /2014/02/27/siunitx-development-notes-for-my-future-self/
categories:
  - Packages
  - siunitx
---
Working on [`siunitx`](https://ctan.org/pkg/siunitx) over the years, I've learnt a lot about units and how people want to typeset them. I've also realised that I've made a few questionable choices in how I've tackled various problems. With one eye to future LaTeX3 work, and another to what I might still improve in `siunitx`, I thought it would be interesting to make a few notes about what I've picked up.

1. Sticking to math mode only would be a good idea. The flexibility that the package offers in terms of using either math or text mode is very popular, but it makes my life very tricky and actually makes some features impossible (TeX only allows us to reliably escape from math mode by using a box). It's also got some performance implications, and the more I've thought about it, the more I realise that it was probably not the best plan to allow both choices.
2. A different approach to the `\boldmath` issue would be sensible. Currently, one of the reasons I use a switch from text to math mode internally is that it allows 'escaping' from `\boldmath`. However, that's probably not the best plan, as it again introduces some restrictions and performance hits, and I think is very unlikely to actually be helpful!
3. The default number parser should be simple and quick: complex parsing should be an option. As it stands, the parser in `siunitx` is quite tricky as it does lots of things. A better approach would be to only deal with digit separation 'out of the box' (so not really parsing at all), and to allow things like uncertainties, complex numbers and the like as add-ons.
4. Tables really need a separate subpackage. Dealing with tables of numbers was never really my aim, and I think much clearer tack would be to have some of the internals of the number parse accessible 'publicly', then build the table functionality up separately.
5. The unit parser works very well: don't change it! Although people ask me mainly about numbers and tables, the real business end of `siunitx` is the unit parser/formatter. It's basically spot-on, with only really minor tune-ups needed.

Probably most of this has to wait for a 'real' LaTeX3 numbers/units bundle: I can't break existing documents. However, I've got a few ideas which can be implemented when I get the time: watch this space.
