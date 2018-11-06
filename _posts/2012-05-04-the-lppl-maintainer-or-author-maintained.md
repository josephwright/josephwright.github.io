---
id: 1361
title: 'The LPPL: &#8216;maintainer&#8217; or &#8216;author-maintained&#8217;'
date: 2012-05-04T10:27:47+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1361
permalink: /2012/05/04/the-lppl-maintainer-or-author-maintained/
categories:
  - General
tags:
  - LPPL
---
The [LaTeX Project Public License (LPPL)](https://www.latex-project.org/lppl/) was written to allow development of LaTeX code in a way that is free as in speech while also making sure that LaTeX users get what they expect when they

```latex
\usepackage{foo}
```

Frank Mittelbach wrote an [excellent overview](https://www.tug.org/members/TUGboat/tb32-1/tb100mitt.pdf) of how the LPPL was developed for [_TUGBoat_](https://tug.org/tugboat/) last year, where he discussed the balance between the rights of the coder and the rights of the person using the code!

The LPPL is designed to deal with packages which are both ‘maintained’ and ‘unmaintained’, and provides a way to allow new maintainers to take over unmaintained material. It also allows for packages to be ‘author-maintained’, which sounds similar to just ‘maintained’ but is significantly different.

Packages which are either ‘maintained’  or  ‘author-maintained’ have one or more people looking after it, and they are responsible for making changes to the code. The difference comes if those people disappear (as has [happened recently with biblatex](/2012/04/03/biblatex-status/)). With a ‘maintained’ package, it's possible for a new person or team to make a public statement that they are going to take over, then after a delay they become the new maintainers. On the other hand, a package which is ‘author-maintained’ cannot be taken over by someone else.

Now, the LPPL is a ‘free’ license and so it is always possible to create a fork from an existing package. In general, you don't really want to do that simply to keep updating an existing package: taking over maintenance is much clearer all round. For biblatex, we can't do that as it's ‘author-maintained’. So we're going to have to [formally fork the project](/2012/04/23/biblatex-a-team-to-continue-the-work/), mark the ‘new’ version as distinct from the old (Philipp Lehman) version and ensure that both remain on CTAN: not ideal.

So I'd urge people to mark their LPPL code as ‘maintained’  rather than  ‘author-maintained’.  You never know what might happen, and ‘maintained’ status works pretty well.
