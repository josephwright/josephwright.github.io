---
id: 476
title: What does \write18 mean?
date: 2009-10-06T21:50:18+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=476
permalink: /2009/10/06/what-does-write18-mean/
categories:
  - General
---
I recently talked about <a href="http://www.texdev.net/2009/09/28/eps-graphics-with-pdflatex/">converting eps files to pdf format</a>, and mentioned that to do it from within TeX, you need <code>\write18</code> enabled. However, I failed to say what that means: probably not very helpful.

The TeX <code>\write</code> primitive instruction is used to write to different file ‘streams’; TeX refers to each open file by number, not by name (although most of the time we hide this). Stream 18 is special: it is not a file but means that TeX asking the operative system to do something. To run a command, we put it as the argument to <code>\write18</code>. So to run the epstopdf program on a file with name stored as <code>\epsfilename</code>, we'd do:
<pre>\write18{epstopf \epsfilename}</pre>
When using something like the epstopdf LaTeX package, that is hidden away and you don't need to worry about the exact way it's done. I'm not going to worry about the detail of the <code>\write</code> instruction here!

However, there is a security issue. If you download some TeX code from the Internet, can you be sure that there is not some command in it (perhaps in a hidden way) to do stuff that might be harmful to your PC (lets say delete everything on the hard disk!). So both <a title="MiKTeX Homepage" href="http://www.miktex.org">MiKTeX</a> and <a title="TeX Live" href="http://www.tug.org/texlive/">TeX Live</a> have traditionally disabled <code>\write18</code> as standard. To turn it on, both support an additional argument when starting TeX:
<pre>(pdf)(la)tex --shell-escape</pre>
The problem with this is that most people use (La)TeX via a graphical editor, and each one needs the correct settings changing to use <code>\write18</code> for every file. It's also not such a great idea to turn it on for everything: it rather defeats the point of it being off by default!

The latest version of MiKTeX (2.8), and the upcoming TeX Live release (2009) get around this by having a special ‘limited’ version of <code>\write18</code> enabled ‘out of the box’. The idea is to allow only a pre-set list of commands (for example, BibTeX, epstopdf, TeX itself, and so on). Those on the list are regarded as safe enough to allow, whereas anything else (for example deleting files) still needs to be authorised by the user. This seems to be a good balance: most people most of the time will not need to worry about <code>\write18</code> at all, but it will be available for things like epstopdf.
