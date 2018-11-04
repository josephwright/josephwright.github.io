---
id: 1862
title: TeXworks developments
date: 2016-02-27T09:58:46+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1862
permalink: /2016/02/27/texworks-developments/
categories:
  - TeXworks
---
Over recent weeks, Stefan Löffler has provided <a href="https://drive.google.com/folderview?id=0B5iVT8Q7W44pNDlQVm9uRGpEWHc&amp;tid=0B5iVT8Q7W44pMkNLblFjUzdQUVE">new builds</a> for <a href="https://www.tug.org/texworks/">TeXworks</a>
featuring a re-implementation of the PDF view. This offers
new modes for previewing the output, most notably continuous scrolling.
It's also intended to be much faster than the older viewer.

Stefan's also been setting up Travis-CI testing for TeXworks, and this
has the added benefit that he's now able to provide <a href="https://bintray.com/stloeffler/generic/Latest-TeXworks-Mac/_latestVersion">Mac binaries</a> in addition
to Windows and Linux ones. Stefan himself doesn't have a Mac for testing
them, but Travis-CI can run automated tests. Moreover, individual users
can grab the burning edge code and use it themselves.