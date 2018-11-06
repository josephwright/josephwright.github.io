---
id: 1103
title: ConTeXt in MacTeX 2011
date: 2011-09-10T11:57:52+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1103
permalink: /2011/09/10/context-in-mactex-2011/
categories:
  - General
tags:
  - ConTeXt
  - MacTeX
---
I recently stumbled across an issue with my <a href="http://wiki.contextgarden.net">ConTeXt</a> set up, while looking at a <a href="http://tex.stackexchange.com/q/27952/73">question about Tikz and ConTeXt</a>. While ConTeXt Mark II was fine, I got the rather cryptic error:
<pre>mtxrun          | forcing cache reload
resolvers       | resolving | configuration files already identified
resolvers       | resolving | skipping configuration file
'selfautoparent:/texmfcnf.lua' (no content)
resolvers       | resolving | no texmf paths are defined (using TEXMF)
resolvers       | resolving |
mtxrun          | the resolver databases are not present or outdated
resolvers       | resolving | using suffix based filetype 'lua'
resolvers       | resolving | using suffix based filetype 'lua'
resolvers       | resolving | remembered file 'mtx-context.lua'
resolvers       | resolving | using suffix based filetype 'lua'
mtxrun          | unknown script 'context.lua' or 'mtx-context.lua'</pre>
when trying to run ConTeXt Mark IV. It seems that this because I installed <a href="http://www.tug.org/mactex">MacTeX 2011</a> during pre-testing. A quick e-mail to the ConTeXt mailing list pointed to the file <code>/usr/local/texlive/2011/texmfcnf.lua</code>, which for me read
<pre>-- (Public domain.)
-- This texmfcnf.lua file should exist only if you have personal changes
-- from the distributed file; for example, if TEXMFVAR was changed in
-- the installer.
--
return { TEXMFCACHE = '~/Library/texlive/2011/texmf-var' }</pre>
It seems that this is defective, as replacing the content with
<pre>
return {
  content = {
    variables = {
      TEXMFHOME = "~/Library/texmf",
      TEXMFVAR = "~/Library/texlive/2011/texmf-var",
      TEXMFCONFIG = "~/Library/texlive/2011/texmf-config",
    },
  },
}
</pre>
(as suggested by Mojca Miklavec) sorted the issue straight away.
