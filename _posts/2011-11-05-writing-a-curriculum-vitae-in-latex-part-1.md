---
id: 1131
title: 'Writing a curriculum vitae in LaTeX: Part 1'
date: 2011-11-05T22:40:53+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1131
permalink: /2011/11/05/writing-a-curriculum-vitae-in-latex-part-1/
categories:
  - General
tags:
  - curriculum vitae
  - résumé
---
Writing a <em>curriculum vitae</em> (what Americans would call a <em>résumé</em>) is something that most of us have to do when applying for jobs. LaTeX users will naturally want to do this using LaTeX. Beyond the technical detail, there's also the question of the wider requirements for a CV: while these are not LaTeX-related, they do form an important part of the process. So here I'd like to look first at the big picture, and then at some of the LaTeX approaches available.
<h2>What is a CV?</h2>
Before we look at writing a CV, it's important to be clear on what its for. Broadly, a CV is a condensed and (hopefully) easy-to-read summary of your qualifications and job experience. Most people want their CV to look good, but it's important to remember that most employers have a tick list of items to find, and the look is probably of marginal importance in most cases. Of course, LaTeX users will still want to take the time to get a great visual result. (If you are applying for a job with a heavy dependence on visual design, then appearance may be the key!)

The other thing to bear in mind is that the requirements for a CV are dependent on the country and subject area you are in. Here in the UK, the normal advice is that a CV should only be two pages long. For academic jobs (like mine), a list of publications will often make the CV longer, while for industrial positions statements about your abilities, non-work activities and so forth are common. There's also a strong feeling <em>against</em> having a photograph, both here in the UK and in the US, for equal opportunities reasons. On the other hand, several other countries have very different conventions, so before you start it's important to check on what is needed.

Each job you apply for is different, and that means each CV you send of should be targeted to that job if possible. So while the basic structure will vary slowly, you should consider what to emphasise in each application. That's an area where LaTeX's ability to comment out lines can be a real bonus.
<h2>Classes</h2>
As a CV is a specialist type of document, it's no surprise that <a title="TUGBoat  Vol 32, No. 2: Highlights" href="http://www.ctan.org/">CTAN</a> features a number of dedicated classes. I'm seen a few questions recently about <a href="http://ctan.org/pkg/moderncv">moderncv</a>, while in the past I used <a href="http://ctan.org/pkg/curve">CurVe</a>. In these and other cases, the idea is to use a mix of standard mark up and specialist macros to construct the output. In most cases, there is some form of tabular-like appearance generated along with the necessary headings and so on.

There are advantages and disadvantages to using one of these classes. Most obviously, someone else provides both the mechanisms you need and (hopefully) a good example to start from. The problem tends to be that altering the layout can be a bit awkward. As I said, while CV appearance may not actually be vital, most of us want to make our CV ‘personal’, which means altering the appearance.
<h2>Roll-your-own</h2>
The alternative to using a pre-built class is to construct your CV yourself, setting up a structure that makes sense to you. Now, there is a bit of effort needed to do this, but it does allow you to decide on exactly how things will look. For my <a href="http://www.texdev.net/wp-content/uploads/2011/11/cv.pdf">own CV</a>, I used to use CurVe, but in the end decided this was actually making my life more, not less, complex. So the <a href="http://www.texdev.net/wp-content/uploads/2011/11/cv.tex">current source</a> is based on the standard article, using some custom macros.

Most of what I've done in my CV is pretty simple, but it's always nice to have documented examples. That would probably make this post a little too long, so I'll return to look at the detail in my next post.