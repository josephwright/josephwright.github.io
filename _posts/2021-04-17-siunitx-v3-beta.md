---
title: siunitx v3 beta
layout: post
permalink: /2021/04/16R/siunitx-v3-beta
categories:
  - siunitx
---

I've been talking about a new version of
[`siunitx`](https://ctan.org/pkg/siunitx) for
[ages](/2019/11/02/siunitx-v3-alpha-2/). Progress has been slot but I've now put
my back into it and got to a feature-complete version: I'm calling this
v3.0.0-beta. As this is a beta release, it's not ready for production just
yet, but it is ready for proper testing. I've made the TDS-style zip file
[available here](/uploads/2021/04/17/siunitx-v3.0.0-beta.tds.zip); if you
know how to use this kind of file, please download and test!

As I've said before, there are a lot of internal improvements in the code.
There are also some big changes which do show to users. The major changes
are

- The name for commands for units and quantities have changed:
  `\unit` and `\qty`. The old names are still about, but I'd encourage
  people to move to the new ones.
- Font set up is entirely revised, which means that there are new settings
  to use if you want to adjust the output. The new approach should be faster
  and cleaner than the old one, but you might have to pick new options.
- Products of numbers now have a dedicated interface: `\numproduct`, with
  a matching `\qtyproduct` for quantities
- Complex numbers also have decided interfaces: `\complexnum` and `\complexqty`:
  this makes parsing a _lot_ easier
- A small number of ideas have been removed: most notably parsing quotients

To support users and to avoid breaking any documents, the new code is
accompanied by a (likely) final version 2 file. That can be loaded using
```latex
\usepackage{siunitx}[=v2]
```
where needed.

What I'm looking for now is feedback on what works, what I've missed, _etc._
Feedback is best in [issues on
GitHub](https://github.com/josephwright/siunitx/issues). You might notice
I'm already planning v3.1 and v3.2: the new structures should make more
development possible. But at the moment I'm mainly trying to finalise
v3.0.
