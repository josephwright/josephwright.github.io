---
title: The beamer slide overlay concept
layout: post
permalink: /2014/01/17/the-beamer-slide-overlay-concept/
categories:
  - beamer
tags:
  - overlays
---
There was a [question recently](https://tex.stackexchange.com/questions/154521) on the [TeX StackExchange site](https://tex.stackexchange.com) about the details of how slide overlays work in the [`beamer`](https://ctan.org/pkg/beamer) class. The question itself was about a particular input syntax, but it prompted me to think that a slightly more complete look at overlays would be useful.

A word of warning before I start: don't overdo overlays! Having text or graphics appear or disappear on a slide can be useful but is easy to over-use. I'm going to focus on the mechanics here, but that doesn't mean that they should be used in every `beamer` frame you create.

## Overlay basics

Before we get into the detail of how `beamer` deals with overlays, I'll first give a bit of background to what they are. The `beamer` class is built around the idea of frames:

```latex
\begin{frame}
  \frametitle{A title}
  % Frame content
\end{frame}
```

which can produce one or more slides: pages of output that will appear on the screen. These separate slides within a frame are created using overlays, which is the way the `beamer` manual describes the idea of having the content of individual slides varying. Overlays are 'contained' within a single frame: when we start a new `frame`, any overlays from the previous one stop applying.

The most basic way to create overlays is to explicitly set up individual items to appear on a particular slide within the frame. That's done using the (optional) overlay argument that `beamer` enables for many document components: this overlay specification is given in angle brackets. The classic example is a list, where the items can be made to appear one at a time.

```latex
\begin{frame}
  \begin{itemize}
    \item<1-> This is on the first and all following slides
    \item<2-> This is on the second and all following slides
    \item<3-> This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
```

As you can see, the overlay specification here is simply the first slide number we want the item to be on followed by a `-` to indicate 'and following slides'. We can make things more specific by giving only a single slide number, giving an ending slide number and so on.

```latex
\begin{frame}
  \begin{itemize}
    \item<1> This is on the first only
    \item<-3> This is on the first three slides
    \item<2-4,6> This is on the second to fourth slides and the sixth slide
  \end{itemize}
\end{frame}
```

The syntax is quite powerful, but there are at least a couple of issues. First, the slide numbers are hard-coded. That means that if I want to add something else in before the first item I've got to renumber everything. Secondly, I'm having to repeat myself. Luckily, `beamer` offers a way to address both of these concerns.

## Auto-incrementing the overlay

The first tool `beamer` offers is the the special symbol `+` in overlay specifications. This is used as a place holder for the 'current overlay', ans is automatically incremented by the class. To see it in action, I'll rewrite the first overlay example without any fixed numbers.

```latex
\begin{frame}
  \begin{itemize}
    \item<+-> This is on the first and all following slides
    \item<+-> This is on the second and all following slides
    \item<+-> This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
```

What's happening here? Each time `beamer` finds an overlay specification, it automatically replaces all of the `+` symbols with the current overlay number. It then advances the overlay number by 1. So in the above example, the first `+` is replaced by a `1`, the second by a `2` and the third by a `3`. So we get the same behaviour as in the hard-coded case, but this time if I add another item at the start of the list I don't have to renumber everything.

There are of course a few things to notice. The first overlay in a frame is number 1, and that's what `beamer` sets the counter to at the start of each frame. To get the second item in the list to appear on slide 2, we still require an overlay specification for the first item: although I used one, I could have skipped the `&lt;1-&gt;` in the hard-coded example and nothing would have changed. The second point is that _every_ `+` in an overlay specification gets replaced by the same value. We'll see later there are places you might accidentally add a `+` to mean 'advance by 1': don't do that!

## Reducing redundancy

Using the `+` approach has made our overlays flexible, but I've still have to be repetitive. Handily, `beamer` helps out there too by adding an optional argument to the list which inserts an overlay specification for each line:

```latex
\begin{frame}
  \begin{itemize}[<+->]
    \item This is on the first and all following slides
    \item This is on the second and all following slides
    \item This is on the third and all following slides
    ...
  \end{itemize}
\end{frame}
```

Notice that this is needs to be inside the 'normal' `[ ... ]` set up for an optional argument. Applying an overlay to every item might not be exactly what you want: you can still override individual lines in the standard way.

```latex
\begin{frame}
  \begin{itemize}[<+->]
    \item This is on the first and all following slides
    \item This is on the second and all following slides
    \item This is on the third and all following slides
    \item<1-> This is on the first and all following slides
    ...
  \end{itemize}
\end{frame}
```

Remember not to overdo this effect: just because it's easy to reveal every list line by line doesn't mean you should!

## Repeating the overlay number

The `+` syntax is powerful, but as it always increments the overlay number it doesn't allow us to remove the hard-coded numbers from a case such as

```latex
\begin{frame}
  \begin{itemize}
    \item<1-> This is on the first and all following slides
    \item<1-> This is also on the first and all following slides
    \item<2-> This is on the second and all following slides
    \item<2-> This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

For this case, `beamer` offers another special symbol: `.`.

```latex
\begin{frame}
  \begin{itemize}
    \item<+-> This is on the first and all following slides
    \item<.-> This is also on the first and all following slides
    \item<+-> This is on the second and all following slides
    \item<.-> This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

What happens here is that `.` can be read as 'repeat the overlay number of the last `+`'. So the two `+` overlay specifications create two slides, while the two lines using `.` in the specification 'pick up' the overlay number of the preceding `+`. (The `beamer` manual describes the way this is actually done, but I suspect that's less clear than thinking of this as a repetition!)

Depending on the exact use case, you might want to combine this with the 'reducing repeated code' optional argument, with `&lt;.-&gt;` as an override.

```latex
\begin{frame}
  \begin{itemize}[<+->]
    \item This is on the first and all following slides
    \item<.-> This is also on the first and all following slides
    \item This is on the second and all following slides
    \item<.-> This is also on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

## Offsets

A combination of `+` and `.` use can be used to convert many 'hard-coded' overlay set ups into 'relative' ones, where the slide numbers are generated by `beamer` without you having to work them out in advance. However, there are cases it does not cover. To allow even more flexibility, `beamer` has the concept of an 'offset': and adjustment to the number that is automatically inserted. Offset values are given in parentheses after the `+` or `.` symbol they apply to, for example

```latex
\begin{frame}
  \begin{itemize}
    \item<+(1)-> This is on the second and all following slides
    \item<+(1)-> This is on the third and all following slides
    \item<+-> This is also on the third and all following slides
  \end{itemize}
\end{frame}
```

Notice that in this adjustment only applies to the substitution, so both the second and third lines above end up as `&lt;3-&gt;` after the automatic replacement. If you try the demo, you'll also notice that none of the items appear on the first slide!

Perhaps a more realistic example for where an offset is useful is the case of revealing items 'out of order', where the full list makes sense in some other way. With hard-coded numbers this might read

```latex
\begin{frame}
  \begin{itemize}
    \item<1-> This is on the first and all following slides
    \item<2-> This is on the second and all following slides
    \item<1-> This is on the first and all following slides
    \item<2-> This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

which can be made 'flexible' with a set up such as

```latex
\begin{frame}
  \begin{itemize}
    \item<+-> This is on the first and all following slides
    \item<+-> This is on the second and all following slides
    \item<.(-1)-> This is on the first and all following slides
    \item<.-> This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

or the equivalent

```latex
\begin{frame}
  \begin{itemize}
    \item<+-> This is on the first and all following slides
    \item<.(1)-> This is on the second and all following slides
    \item<.-> This is on the first and all following slides
    \item<+-> This is on the second and all following slides
    ...
  \end{itemize}
\end{frame}
```

As shown, we can use both positive and negative offsets, and these work equally well for `+` and `.` auto-generated values. You have to be slightly careful with negative offsets, as while `beamer` will add additional slides for positive offsets, if you offset below a final value of `0` then errors will crop up. With this rather advanced set up, which version is easiest for you to follow will be down to personal preference.

Notice that positive offsets _do not_ include a `+` sign: remember what I said earlier about _all_ `+` symbols being replaced. If you try something like `&lt;+(+1)&gt;`, your presentation will compile but you'll have a _lot_ of slides!

## Summary

The `beamer` overlay specific can help you set up complex and flexible overlays to generate slides with dynamic content. By using the tools carefully, you can make your input easier to read and maintain.
