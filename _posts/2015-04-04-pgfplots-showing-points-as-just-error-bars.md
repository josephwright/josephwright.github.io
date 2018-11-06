---
id: 1809
title: 'pgfplots: Showing points as just error bars'
date: 2015-04-04T22:11:07+00:00
author: josephwright
layout: post
guid: http://www.texdev.net/?p=1809
permalink: /2015/04/04/pgfplots-showing-points-as-just-error-bars/
categories:
  - General
tags:
  - pgfplots
---
Presenting experimental work in a clear form is an important skill. For plotting data, I like the excellent [`pgfplots`](https://ctan.org/pkg/pgfplots) package, which makes it easy to put together consistent presentations of complex data. At the moment, I'd doing some experiments where showing the error bars on the raw data is important, but at the same time to show fit lines clearly. The best style I've seen for this is one where the data are show as simple vertical bars which have length determined by the error bars for the measurements. The fit lines then stand out clearly without overcrowding the plot. That style isn't built in to `pgfplots` but it's easy to set up with a little work:

```latex
\documentclass{standalone}
\usepackage{pgfplots}

% Use features from current release
\pgfplotsset{compat = 1.12}

% Error 'sticks'
\pgfplotsset{
  error bars/error mark options = {draw = none}
  % OR more low-level
  % error bars/draw error bar/.code 2 args = {\draw #1 -- #2;}
}

\begin{document}
\begin{tikzpicture}
  \begin{axis}
    [
      error bars/y dir      = both,
      error bars/y explicit = true,
    ]
    \addplot[draw = none] table[y error index = 2]
      {
        0   0.023 0.204
        1   0.956 0.332
        2   4.234 0.552
        3   8.764 0.345
        4  17.025 0.943
        5  27.201 2.445
      };
    \addplot[color = red, domain = 0:5, samples = 100] {x^2};
  \end{axis}
\end{tikzpicture}
\end{document}
```

![](/wp-content/uploads/2015/04/test-300x248.png)
My demo only has a few data points, but this style really shows it's worth as the number of points rises.
