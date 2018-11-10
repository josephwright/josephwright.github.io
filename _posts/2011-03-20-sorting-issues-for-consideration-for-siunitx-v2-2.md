---
title: Sorting issues for consideration for siunitx v2.2
layout: post
permalink: /2011/03/20/sorting-issues-for-consideration-for-siunitx-v2-2/
categories:
  - Packages
  - siunitx
---
I've been leaving [`siunitx`](https://ctan.org/pkg/siunitx) alone for a while, concentrating on bug fixes in the v2.1 branch. The  [list of issues](https://github.com/josephwright/siunitx/issues?status=open) has continued to grow, and I'm now getting some organisation done before starting on items for v2.2. Some of these are more likely to get tackled, some rather less likely, but it's best to get everything logged! If you look at the [closed issues](https://github.com/josephwright/siunitx/issues?status=closed), you'll see that part of getting organised is closing some bugs where I don't feel that it is appropriate to take action. What I would say is that if you've got something you'd like considering, put it into the database. I do try to keep up with ideas by [e-mail](mailto:joseph.wright@morningstar2.co.uk) or from forums, but do forget some.

On particular thing I want to think about is the naming is some options and macros. I've had some discussion with Marcus Foster from [CSIRO Information Management &amp; Technology](http://www.csiro.au/) about `siunitx`, and he's pointed out various errors on my part. Some of those, in the documentation, have been fixed. At the code level, he pointed out that what `\SI` prints are properly called quantities, and that units are separated by products. So I'm thinking of some reasonably radical renaming of [macros](https://github.com/josephwright/siunitx/issue/116/) and [options](https://github.com/josephwright/siunitx/issue/115/) (with the old ones retained, of course!). Feedback on these ideas would be welcome. At the same time, he's not at all keen on the 'qualifiers' concept, but on that I think users would not be happy if I removed it!
