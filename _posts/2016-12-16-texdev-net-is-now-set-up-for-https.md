---
id: 1906
title: texdev.net is now set up for https
date: 2016-12-16T17:56:13+00:00
author: josephwright
layout: post
guid: https://www.texdev.net/?p=1906
permalink: /2016/12/16/texdev-net-is-now-set-up-for-https/
categories:
  - texdev.net
tags:
  - https
---
A rare foray outside of the strictly TeX-related: as it's about the blog itself I think its OK! As you might notice on visiting the site, I've enabled https for the site. Why have I done that? Well, if you read the [WordPress News](https://wordpress.org/news/2016/12/moving-toward-ssl/) it's clear that they are pushing toward more use of secure access. (As you might guess, the back-end for the blog is WordPress.) There are wider moves toward ['https everywhere'](https://www.eff.org/https-everywhere%20), so it seemed like as good a time as any to do the work.

For readers, there should be no change at all in the site. For those interested in the detail, I've moved the hosting to [SiteGround](https://www.siteground.co.uk/) as they offer [Let's Encrypt](https://letsencrypt.org/): a free SSL certificate system suitable for small-scale sites like this one. (If anyone is feeling particularly generous, I've got a [referral URL](http://www.siteground.com/recommended?referrer_id=7485305) which will give me some free service in return for pointing to my new host!) The process was largely trouble-free: I've taken the opportunity to re-build the site from scratch (just using the dumps of the content) and to remove some older 'back-end' rubbish (old plugins and the like). Again, for readers this should be transparent!