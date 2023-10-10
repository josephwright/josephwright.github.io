---
title: A LaTeX format beyond LaTeX2e
layout: post
permalink: /2012/02/21/a-latex-format-beyond-latex2e/
categories:
  - expl3
tags:
  - LuaTeX
---
The question of why[ LaTeX3 development is not focussed on LuaTeX](https://tex.stackexchange.com/questions/45183/latex3-versus-pure-lua) came up yesterday on the [TeX-sx](http://tex.blogoverflow.com/) site. I've added an answer there covering some of the issues, but I thought that something a bit more open-ended might also be useful on the same topic.

Before I look at the approaches that are available, it's worth asking why a format is needed beyond LaTeX2e. There are a few reasons I feel it's needed, but a few stand out.

The first, strangely, is stability. LaTeX2e is stable: there will be no changes other than bug fixes. That means that a document written 10 or more years ago should still give the same output when typeset today. That sounds great, but there is an issue here. While the kernel is stable, packages are not, and the limitations of the kernel mean that there are a lot of packages. So for a lot of real documents, stability in the kernel does not mean that they will still work after many years, at least without some effort. So we need a kernel which provides a lot more of the basics, and perhaps new approaches to providing stable code.

Secondly, and related, is the fact that most real documents need a lot of packages, and that is a barrier to new users. Again, stability is great but not if it means we don't continue to attract new people to the LaTeX world. I think that the LaTeX approach is a good one, so that is important to me. So I feel that we need a format which works well and provides a lot more functionality as standard.

Thirdly, there are some fundamental issues which are hard to address, such as inter-paragraph spacing, the placement of floats and better separation of design from input. There all need big changes in LaTeX, and it's not realistic to hope to bolt such changes on to LaTeX2e and have everything continue to work.

All of that tells me we need a new kernel. So the question is how to achieve that. There are at least four programming approaches I've thought about.

Two are closely related: stick with TeX macro programming and cross-engine working, but make things more systematic. Perhaps the simplest way to do this is to adopt an approach similar to the [`etoolbox`](https://ctan.org/pkg/etoolbox) package, and to essentially add to the structures already available. The more radical approach in the same area is to do what the LaTeX3 Project have to date, and define a new programming language from the ground up using TeX macros.  There are arguments in favour of both of these approaches: I've done some experiments with a more `etoolbox`-like method for creating a format. My take here is that if you really want something more systematic than LaTeX2e then you do have to go to something like the LaTeX3 method: dealing with expansion with names like `\csletcs` gets too unwieldy as you try to construct an entire format.

Moving to a LuaTeX-only solution, and doing a lot of the programming in Lua, is the method that the [ConTeXt](http://wiki.contextgarden.net/) team has decided on. This brings in a proper programming language without any direct effort, but leaves open some issues Using Lua does not automatically solve the challenges in writing a better format, and using LuaTeX does not mean not that there is no TeX programming to do. So a LuaTeX-only approach would still need some TeX work.

Finally, there is the argument for parsing LaTeX-like input in an entirely new way. In this model, you don't use TeX at all to read the user's input: that's done by another language, and TeX is only involved at all when you do the typesetting. That sound challenging, and the big issue here is finding someone who has the necessary programming skills (I certainly do not).

Of the four approaches, it seems to me that from where we are now, the LaTeX3 approach is not so bad. If you were starting today with no code at all, and not background in programming `expl3` or Lua, you might pick the LuaTeX method. That's not, however, where we are: there is experience of `expl3` available, and there is also code written (but in need of revision). Of course, the proof of that will be in delivering a working LaTeX3 format: on that, back to work!
