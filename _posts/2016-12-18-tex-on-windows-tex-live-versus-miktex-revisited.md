---
title: 'TeX on Windows: TeX Live versus MiKTeX revisited'
layout: post
permalink: /2016/12/18/tex-on-windows-tex-live-versus-miktex-revisited/
categories:
  - General
tags:
  - MiKTeX
  - TeX Live
  - Windows
---
On Windows, users have two main choices of TeX system to install: [TeX Live](https://tug.org/texlive) or [MiKTeX](https://miktex.org). I've looked at this before a couple of times: first in [2009](/2009/11/07/windows-tex-users-miktex-or-tex-live/) then again in [2011](/2011/11/19/tex-on-windows-miktex-or-tex-live/). Over the past few years both systems have developed, so it seems like a good time to revisit this. (I know from my logs that this is one of the most popular topics I've covered!)

The first thing to say is that for almost all 'end users' (with a TeX system on their own PC just for them to use), both options are fine: they'll probably notice no difference between the two in use. It's also worth noting that there is a third option: [W32TeX](http://w32tex.org/). I've mentioned this before: it's popular in the far East and is where the Windows binaries for TeX Live come from. (There's a close relationship between W32TeX and TeX Live, with W32TeX more 'focussed' and expecting more user decisions in installing.)

Assuming you are going for one of the 'big two', what is there to think about? For most people, it's simply:

- Both MiKTeX and TeX Live include a 'full' set of TeX-related binaries, including the engines pdfTeX, XeTeX, LuaTeX and support programs such as BibTeX, Biber, MakeIndex and Xindy.
- The standard installer for MiKTeX installs 'just the basics' and uses on-the-fly installation for anything else you need; the standard install for TeX Live is 'everything' (about 4.5 Gb!). Which is right for you will depend on how much space you have: you can of course customise the installation of either system to include more or less of the 'complete' set up.
- MiKTeX has a slightly more flexibly approach to licensing than TeX Live does: there are a small number of LaTeX packages that MiKTeX includes that TeX Live does not. (Probably the most obvious example is [`thesis`](https://ctan.org/pkg/thesis).)
- TeX Live has a Unix background so the management GUI looks slightly less 'standard' than the MiKTeX one.
- TeX Live has a strict once-a-year freeze,which means that to update you have to do a fresh install once a year. On the other hand, MiKTeX versions change only when there is a significant change and otherwise 'roll onward'.

So the decision is likely to come down to whether you want auto-installation of packages. (If you do go for MiKTeX on a one-user PC, choose the 'Just for me' installation option: it makes life a lot simpler!)

For more advanced users there are a few more factors you probably want to consider

- TeX Live was originally developed on Unix and so is available for Linux and on the Mac (and other systems) as well as Windows; MiKTeX is a Windows system so is (more-or-less) Windows-only. So if you want exactly the same set up on Windows and other operating systems, this of course means you need to use TeX Live.
- Both systems have graphical management tools as well as command line interfaces. They have a lot in common, but they are not identical (in particular, MiKTeX tends to emulate TeX Live command line interfaces, but the reverse is not true).
- The engine binaries in TeX Live are (almost) never updated other than in the yearly freeze period, meaning that for a given release you know which version of pdfTeX, _etc_., you'll have: MiKTeX is more flexible with such updates. (At different times, one or other of the systems can be more 'up to date': this is not necessarily predictable! The [W32TeX](http://w32tex.org/) system often has very up-to-date testing binaries.)
- The two systems differ slightly in handling how local trees are managed (places to add TeX files that are not controlled by the TeX system itself). TeX Live automatically expects `&lt;installation root&gt;/texmf-local` to hold system-wide 'local' additions and `&lt;user root&gt;/texmf` to hold per-user additions, whereas MiKTeX has no out-of-the box locations, but does make it easier to add and remove them from the command line. MiKTeX also makes it easy to add multiple per-user trees, whereas for TeX Live there's more of an assumption that all user additions will be added in one place. (This makes it easier in MiKTeX to add/remove local additions by altering a setting in the TeX system rather than deleting files.)
- TeX Live has a team doing the work; MiKTeX is a one-man project. This cuts both ways: you know exactly who is doing everything in MiKTeX (Christian Schenk), and he's very fast, but there is more 'spread' in TeX Live for the work.
- For people wanting to step quickly between different versions of TeX system, the fact that TeX Live freezes once a year makes life convenient (I have TeX Live 2009,2010, 2011, 2012, 2013, 2014, 2015 and 2016 installed at present, plus MiKTeX 2.9 of course!) You can switch installations by adjusting the `PATH` or by choosing the appropriate version from your editor, so have a 'fall back' if there is an issue when you update.
- TeX Live has build-in package backup during maintenance updates.

