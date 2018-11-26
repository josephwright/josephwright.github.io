---
title: Blog on the move
layout: post
permalink: /2018/11/26/blog-on-the-move/
categories:
  - texdev.net
---

I've been writing _Some TeX Developments_ for ten years now, [starting off](/2008/12/17/some-tex-developments) on
[WordPress.com](http://wordpress.com) before moving to a self-hosted WordPress
set up. All of this time, I've stuck with WordPress as it's a very powerful
and flexible system. However, it's got some downsides too. In particular, as
it is dynamic, database-driven, system, the pages are created each time someone
requests them. That's great for things like supporting comments, but it means
there's a non-trivial amount of work done each time someone views a page. That
turns into a real cost when you are paying for your own hosting. My [most
recent hosts](https://www.siteground.co.uk) were really good for support, but I
needed enough CPU cycles to push me into the 'non-trivial' cost bracket. At
the same time, a dynamic site means that there's always a security risk.

## Enter GitHub Pages

I'm hardly the only person to come across these issues, and it's no surprise
that there are a variety of good solutions. One that's really gained in
popularity over recent years is GitHub Pages. This uses a specially-named Git
repository to run a generation system called [Jekyll](https://jekyllrb.com/).
Unlike WordPress, Jekyll generates pages when the sources are committed, so
the pages themselves are static 'classical' HTML.

## Rinse and repeat

To go from WordPress to Jekyll, I started by extracting all of the content
using the [WordPress to Jekyll Exporter
plugin](https://ben.balter.com/wordpress-to-jekyll-exporter/). That gave me
a set of HTML files which nearly worked straight away (but with no styling).
After a few bits of clean-up to make things work at all, I then did a _load_
of search-and-replace steps. Most of these were to convert the content to
Markdown, clean up minor mark-up issues, _etc._. I also took the opportunity
to work on fixing typos, broken links and so on: that is a lot easier to
do with a local set of files, compared to WordPress.

Most of that work was very mechanical, but it took a while: most of that was
because of flaws in my original text, not the exporter!

## What's missing?

Exporting the content doesn't deal wit the website style, nor does it include
comments. The latter don't work in Jekyll directly, though one can use
[Disqus](https://disqus.com/). I decided against that for the present: I don't
really need a discussion system for my blog.

Getting the style right could have been sorted by copy-pasting the raw HTML
from the old site. But I decided to take the opportunity to revise the
layout. At the present, it's based on the [LaTeX
Project](https://latex-project.org) one, but rather simplified. I may well look
at this again, fixing minor issues as I go. But I'm no design expert: I'd be
very happy to have suggestions!

The final thing to do is to get the web address sorted. I'm just sorting out
with my registrar and GitHub, and that will be done shortly. Hopefully, with
that done, my latest blog rearrangements will be done!
