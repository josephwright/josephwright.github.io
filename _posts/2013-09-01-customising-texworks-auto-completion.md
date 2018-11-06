---
id: 1641
title: Customising TeXworks auto-completion
date: 2013-09-01T09:45:37+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1641
permalink: /2013/09/01/customising-texworks-auto-completion/
categories:
  - TeXworks
---
[TeXworks](https://tug.org/texworks) is a very flexible editor, and one of the things you can customise, if you want, is the set of auto-completion values it knows. For those of you who are not familiar with it, TeXworks uses a simple list of simple completion options, so when I type

```latex
\doc
```

I can press the Tab key and be offered

```latex
\documentclass{}
```

and if I press Tab again,

```latex
\documentclass[]{}
```

That's very useful, but some of the auto-complete options are not ones I use a lot. There are also a few inconsistencies in how the results are formatted: while TeXworks inherited a basic set from [TeXShop](http://pages.uoregon.edu/koch/texshop/‎), it also comes with some additions and they don't always quite agree on how things should work! So I've been looking a bit at sorting out my own custom set, adding things I use, removing ones I don't and so on.

The basic format for the auto-complete files is to have a first line for the encoding

```latex
%% !TEX encoding = UTF-8 Unicode
```

then one or more lines for each completion. Each line can either just have a completion vale

```latex
\alpha
```

or have a 'shortcut' text version

```latex
xa:=\alpha
```

There are then a few bits of 'helper' syntax. You can use `#INS#` to show where the cursor should end up, `#RET` for a return and `•` as a marker you can jump to using Ctrl-Tab (Option-Tab on the Mac). So for example the `\documentclass` lines read

```latex
\documentclass{#INS#}#RET#
\documentclass[#INS#]{•}#RET#
```

I'm told that TeXShop has extended the syntax a bit, but at least at the moment in TeXworks that all there is to know.

So what have I done to customise the files? TeXworks comes with four auto-complete files, but the values offered simply come from them all together (you can't currently select only some files). (You might wonder where these files live: they are 'hidden away': TeXworks will tell you how to find them from Help -> Settings and resources.)  So my first move was to create one new file, after first backing up the originals of course! I then did a few experiments, thinking about what I use a lot, what I'm used to, _etc_. I did wonder about some of the choices in the standard files, but a bit of experimentation suggests they are not so bad! So I've currently ended up mainly just adding a few things, for example

```latex
{tikzpicture}[#INS#]#RET#•#RET#\end{tikzpicture}•
```

for TikZ pictures and

```latex
cs:=\cs{#INS#}
pkg:=\pkg{#INS#}
\cs{#INS#}
\pkg{#INS#}
```

for package development work. I'm also not too keen on having too many of the 'shortcut' values, which don't start `\`, so I've removed most of them and have just a core set (things like `bf` and `em`). If you want to see my current full set, you can of course [download it](/wp-content/uploads/2013/09/tw-completion.txt).

So is there anything I'd like to see added to the way auto-complete works? I have a few ideas! From my questions on the TeXworks mailing list, I've picked up that TeXShop maintains indentation when doing auto-complete: TeXworks doesn't, and I think it would be a good addition. TeXShop also allows an extended syntax

```latex
\documentclass[#INS#•#INS#]{•}#RET#
\rule[#INS#•‹lift›#INS#]{•‹width›}{•‹height›}
```

where you can always have a `•` for 'fill in' and have 'reminders' about what the values are. That looks useful too.
