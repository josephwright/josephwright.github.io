---
title: Testing versions of siunitx v2.1 on TLcontrib
layout: post
permalink: /2010/10/12/testing-versions-of-siunitx-v2-1-on-tlcontrib/
categories:
  - Packages
  - siunitx
tags:
  - TLcontrib
---
I'm working on the [list of issues](https://github.com/josephwright/siunitx/issues?status=new&amp;status=open&amp;milestone=v2.1) for [`siunitx`](https://ctan.org/pkg/siunitx) v2.1. As I do, I hope that the code is staying usable at all times! The list is getting shorter (finally), so I'm hoping to get something released around the end of the month.  One thing that I need for that is testing. My [recent post about TLcontrib](/2010/10/09/tex-live-packaging-expands/) mentioned this as a route for testing packages prior to release. So I'm taking advantage, and sending snapshots of `siunitx` to TLcontrib each time I add a new feature. So if you want to help to test things out, then you can run

```bash
tlmgr --repository http://tlcontrib.metatex.org/2010 update `siunitx`
```

from your command prompt/terminal. Let me know about any new issues!
