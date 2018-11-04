---
id: 1708
title: Lua for LaTeX3 build scripts
date: 2014-05-25T18:27:04+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1708
permalink: /2014/05/25/lua-for-latex3-build-scripts/
categories:
  - LaTeX3
tags:
  - expl3
  - Lua
  - scripts
---
Anyone who follows the <a href="https://github.com/latex3/svn-mirror">LaTeX3 GitHub pages</a> will have seen a lot of checkins recently, not only for the code itself but also for a new set of build scripts. The work should hopefully make us more efficient but also impact on others, directly or indirectly.

Once of the first things I did when I joined the LaTeX3 Project was to write a load of Windows batch scripts for building the code. At the time, most of the rest of the team were using Unix (Linux, Macs, ...) but I was using Windows, so this was quite important. Since then, the team's IT set up has varied a bit but so have the requirements for our scripts, so I've ended up working quite a bit with both the batch files and the Unix Makefiles.

The 'two sets of scripts' approach has a few problems. The most obvious is that we've had to keep the two in synch: not always entirely successful, and not always remembered! At the same time, the 'standard' facilities available on the two systems are different: we've had to require Perl on all platforms, and work out how best to make everything 'looks the same'.

Some recent discussion prompted me to consider some new work on the scripts, but with Lua now available anywhere that has a TeX system (as <code>texlua</code> for script work), it seemed natural to move to an entirely new set up. The plan has been to have one 'master' script for the entire LaTeX3 repository, rather than the 'copy-paste' arrangement we've had to date, and to use very simple 'configuration' files for each separate module. That's worked really well: we've now got <a href="https://github.com/latex3/l3build/blob/master/l3build.lua">one big file</a> covering almost everything, no longer need Perl and have also addressed some of the things that prompted this in the first place! (More on those in another post soon.)

Even if you are not using LuaTeX for day-to-day TeX work, the scripting ability for supporting development is very handy. Lua doesn't cover the OS-dependent stuff, but using our existing script code and a small amount of detection we've been able to work with that. The new scripts are hopefully nice and clear, more flexible than the old ones and most importantly only need changing in one place for each issue.

So how does this impact on others? First, it makes it easier for the team to work on LaTeX3, which should be a good thing all round. The scripts should also mean that we don't have the odd strange change depending on which operating system is used to do a release. Second, we'd like to hope that other TeX developers can take ideas from our scripts for their own work. We're particularly interested in testing TeX code, and I'll come back to that in my next post. Last, and linked to testing, we are picking up some 'interesting' engine-based issues. Those are getting reported, and even if you never use LaTeX we'd hope that will be a benefit!