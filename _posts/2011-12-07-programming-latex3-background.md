---
id: 1201
title: 'Programming LaTeX3: Background'
date: 2011-12-07T22:14:22+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1201
permalink: /2011/12/07/programming-latex3-background/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
Before the [series on programming LaTeX3](/2011/12/06/programming-latex3-introduction/) can really get started, it's going to be important to establish some background, basic concepts and indeed what the aims are. So in this post I'm going cover some of these issues: we won't be seeing any code just yet! The approach I'm aiming to take is to bring in concepts as they are needed: this may mean a few simplifications in the beginning to allow ideas to be developed.

## LaTeX3: What is available now?

The very first thing to cover is what the current status of LaTeX3 is, and what the aim of this series is. Anyone following LaTeX3 development will know that at the moment it's not ready for creating documents independent of LaTeX2e. What is available now is a programming layer: [`l3kernel`](https://ctan.org/pkg/l3kernel). At the same time, one of the aims with LaTeX3 is to clearly separate out programming, design decisions and actually using LaTeX. So what I will be covering here is programming. At the same time, I'll aim to highlight concepts which are not necessarily tied to LaTeX3 programming but which the LaTeX3 Project feel are part of the overall aims of LaTeX3 development.

## The target audience

I have two distinct audiences in mind in writing this series. The first is experienced (La)TeX programmers who want to see what ideas LaTeX3 introduces. These people will be familiar with many basic TeX concepts, and will want to see the relationship between what they are used to and the ‘LaTeX3 way’. The second group is experience LaTeX2e users who want to learn to program LaTeX, and have decided to miss out learning to program TeX first. It's important that the latter group are included: another key aim for LaTeX3 is to provide a complete set of documentation and support without having to say ‘read _The TeXbook_’ as a requirement to make progress.

What both of these groups have in common is lots of experience with LaTeX2e. So I'm going to expect familiarity with LaTeX2e's user syntax, concepts and so on. So that will very much be the baseline: I do hope that the more experienced LaTeX programmers will bear with me.

## Requirements

As I've indicated, programming LaTeX3 currently means works on top of LaTeX2e. So to get started you need a LaTeX2e installation, which for most people means either [TeX Live](https://tug.org/texlive) or [MiKTeX](https://www.miktex.org/). Most of the code in the programming layer of LaTeX3 has been moving to a stable situation for some time, but there are refinements going on all of the time. As a result, I'll be assuming that readers have the latest [CTAN](https://www.ctan.org) releases of [`l3kernel`](https://ctan.org/pkg/l3kernel) and [`l3packages`](https://ctan.org/pkg/l3packages) installed. That can be done by downloading them from CTAN directly, or using the package managers in TeX Live 2011 or MiKTeX 2.9.
