---
title: ConTeXt in MacTeX 2011
layout: post
permalink: /2011/09/10/context-in-mactex-2011/
categories:
  - General
tags:
  - ConTeXt
  - MacTeX
---
I recently stumbled across an issue with my [ConTeXt](http://wiki.contextgarden.net) set up, while looking at a [question about Tikz and ConTeXt](https://tex.stackexchange.com/q/27952/73). While ConTeXt Mark II was fine, I got the rather cryptic error:

```
mtxrun          | forcing cache reload
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
mtxrun          | unknown script 'context.lua' or 'mtx-context.lua'
```

when trying to run ConTeXt Mark IV. It seems that this because I installed [MacTeX 2011](https://tug.org/mactex) during pre-testing. A quick e-mail to the ConTeXt mailing list pointed to the file `/usr/local/texlive/2011/texmfcnf.lua`, which for me read

```lua
-- (Public domain.)
-- This texmfcnf.lua file should exist only if you have personal changes
-- from the distributed file; for example, if TEXMFVAR was changed in
-- the installer.
--
return { TEXMFCACHE = '~/Library/texlive/2011/texmf-var' }
```

It seems that this is defective, as replacing the content with

```lua
return {
  content = {
    variables = {
      TEXMFHOME = "~/Library/texmf",
      TEXMFVAR = "~/Library/texlive/2011/texmf-var",
      TEXMFCONFIG = "~/Library/texlive/2011/texmf-config",
    },
  },
}
```

(as suggested by Mojca Miklavec) sorted the issue straight away.
