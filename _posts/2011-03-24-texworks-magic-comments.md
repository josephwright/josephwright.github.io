---
id: 995
title: 'TeXworks &#8216;magic comments&#8217;'
date: 2011-03-24T08:50:15+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=995
permalink: /2011/03/24/texworks-magic-comments/
categories:
  - TeXworks
---
The [new TeXworks release](http://www.texdev.net/2011/03/21/texworks-v0-4-0/) adds a new ‘magic comment’ to the set that the program knows. So I thought it might be useful to have a list of those that currently work, and a typical setting for each one.

```latex
% !TeX program = LuaLaTeX
```

The name of the typesetting engine to use for the current file, which should be one of the engines that is set up for use with TeXworks. This is useful if you normally use one engine (for example pdfLaTeX), but have a few files that need an alternative engine. In my example, the file would automatically use LuaLaTeX as the engine.

```latex
% !TeX encoding = UTF-8
```

Sets the file encoding for the current file. The usual default is UTF-8, but this setting is handy if you need to collaborate with other people using non-UTF-8 editors.

```latex
% !TeX root = somefile.tex
```

Indicates that the current file is not the main file for typesetting: when you choose to typeset, TeXworks will save the current file then typeset the master file. Using this setting, you need the full name of the master file including the extension. This is clearly a handy setting for larger projects, where you might have a lot of files which are to be included in one master document.

```latex
% !TeX spellcheck = de_DE
```

Specify the spell check language for the current file. This is a new setting in v0.4.0 (it was not present in the 0.2 stable release). The language of course needs to be one you have installed! One point to notice with the

`root` setting is how it interacts with `program`. Let's imagine that the master file needs to be typeset using LuaLaTeX, and that your default engine is pdfLaTeX. You then need to include the `program` in each subsidiary file to get everything to work properly:

```latex
% !TeX root    = master.tex
% !TeX program = LuaLaTeX
```

If you don't do that, when you try to typeset from one of the subfiles then TeXworks will use the currently-selected engine (probably pdfLaTeX) and _not_ LuaLaTeX for the typesetting. Once you know, this is not so surprising, but at first it caught me out!
