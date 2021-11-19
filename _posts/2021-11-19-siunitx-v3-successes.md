---
title: siunitx v3 successes
layout: post
permalink: /2021/11/19/siunitx-v3-successes
categories:
  - siunitx
---

The third major release of [`siunitx`](https://ctan.org/pkg/siunitx) was out [in
May](/2021/06/30/siunitx-v2-to-v3), after the [TeX
Live](https://tug.org/texlive) 2021 DVD. That means it's been picked up
primarily by more active users: people who install TeX between the 'fixed' DVD
releases (or who use [MiKTeX](https://miktex.org)). It also didn't initially
appear on [Overleaf](https://www.overleaf.com), as they take a while to test TeX
Live images before making them public.

I've been making maintenance releases between May and now, and have reached
v3.0.36, picking off small (or less small) issues I'd missed initially. At the
same time, Overleaf now have a TeX Live 2021 image (currently featuring
`siunitx` v3.0.23). So I now have an increasing number of 'normal' users: people
who don't want to deal with testing, and just want their documents to work.

What I notice is that increased usage hasn't raised any truly major issues. Yes,
there have been corrections (see [the
ChangeLog](https://github.com/josephwright/siunitx/blob/main/CHANGELOG.md) for
the detail), but they were mainly at the level of predictable issues: places
that I'd not explored quite enough. I hope Overleaf will consider an in-place
update to somewhere around the latest release: whilst the issues have been
minor in the grand scheme, it would be good to get a reasonably bug-reduced
version out there (I'm not claiming bug-free)!

So I'm seeing the release as in the end quite a big success: I've addressed the
issues I knew about, got better testing, have cleaner interfaces and am already
offering new features. My mind is therefore turning to v3.1: I have a [list of
issues](https://github.com/josephwright/siunitx/issues?q=is%3Aissue+milestone%3Av3.1+)
to consider that I'd like to take for that release, plus I could pick off some
others. I might of course not tackle all of these: I'm thinking starting over
the Christmas period and looking to release in March/April 2022. By then of
course we might be at v3.0.50, so it will also help to 'reset' the path level!
