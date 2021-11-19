---
title: "Programming LaTeX3: More on token list variables"
layout: post
permalink: /2012/01/22/programming-latex3-more-on-token-list-variables/
categories:
  - LaTeX3
tags:
  - Programming LaTeX3
---
In my [previous post](/2011/12/26/programming-latex3-token-list-variables/), I introduced the idea of a _token list variable_, the LaTeX3 term for a macro used to store 'stuff'. Token list variables (tl vars) are the basis of many of the higher level data types in LaTeX3, and they also have arbitrary contents. As a result, there are a lot of generic functions to do things with `tl`vars.

## Adding content, changing content

A very common thing to do with stored material is either to add to it, which we can do either on the left or the right. The LaTeX3 functions to do this are called `\tl_put_left:Nn` and `\tl_put_right:Nn` (and so on), which makes it easy to build up complicated material quite quickly. So

```latex
\tl_new:N \l_my_a_tl
\tl_set:Nn \l_my_a_tl { stuff }
\tl_put_right:Nn \l_my_a_tl { ~here }
\tl_put_left:Nn \l_my_a_tl { My~ }
\tl_use:N \l_my_a_tl
```

will print 'My stuff here'. That's easy enough to do without LaTeX3 coding, but find-and-replace is a bit more involved. So the functions

`\tl_replace_once:Nnn` and `\tl_replace_all:Nnn` are working a little harder:

```latex
\tl_set:Nn \l_my_a_tl { stuff~to~change }
\tl_replace_once:Nnn \l_my_a_tl { change } { alter }
\tl_use:N \l_my_a_tl % 'stuff to alter'
\tl_replace_all:Nnn \l_my_a_tl { t } { q }
\tl_use:N \l_my_a_tl % 'squff qo alqer'
```

## Adding one`tl`var to another

So far, I've added literal input to`tl`vars. That's useful, but a very common task to to combine two or more variables together. To do that, we need a way to access the _content_ of a variable. First, what doesn't work is doing

```latex
\tl_new:N \l_my_b_tl
\tl_set:Nn \l_my_a_tl { stuff }
\tl_set:Nn \l_my_b_tl { ~more~stuff }
\tl_put_right:Nn \l_my_a_tl { \l_my_b_tl }
```

as what ends up inside

`\l_my_a_tl` is `stuff\l_my_b_tl`. This is where LaTeX3's expansion control comes into play. So far, we've seen arguments of type `N` and `n`, but there are others. There are a number of other types, but I want here to introduce just one one: `V`. A `V`-type argument will pass the _value_ of a variable, rather than its name. So the correct way to add the content of one token list variable to another is

```latex
\tl_set:Nn \l_my_a_tl { stuff }
\tl_set:Nn \l_my_b_tl { ~more~stuff }
\tl_put_right:NV \l_my_a_tl \l_my_b_tl
```

which results in `\l_my_a_tl` containing `stuff more stuff`. Now, the LaTeX3 kernel does not provide every possible combination of argument types (although it does provide `\tl_put_right:NV`). That's not a problem, as they can easily be created:

```latex
\cs_generate_variant:Nn \tl_put_right:Nn { NV }
```

This is a 'soft' process: if the variant requested already exists, nothing happens, but otherwise the variant is created. So provided the base function exists, you can always create any variants you need.

## Mappings

Another key idea when working with `tl`vars is the ability to map to each token they contain. For that, there are again a couple of useful functions, `\tl_map_function:NN` and `\tl_map_inline:Nn`. The two differ mainly in _expandability_, a concept we've not covered just yet! I'll be coming back to that in a later post, so for the moment I'll just use `\tl_map_inline:Nn`. What does a mapping do? Try

```latex
\tl_set:Nn \l_my_a_tl { stuff }
\tl_map_inline:Nn \l_my_a_tl { I~saw~'#1'. \\ }
```

and you should get a listing of each separate token in the`tl`var:

> I saw 's'. I saw 't'. I saw 'u’. I saw 'f'. I saw 'f'.

As you can hopefully see, within the second argument of `\tl_map_inline:Nn` the place holder `#1` is used to insert a single token from the`tl`var. For a more complicated`tl`var

```latex
\tl_set:Nn \l_my_a_tl { { stuff } ~ { which } ~ is ~ { complicated } }
\tl_map_inline:Nn \l_my_a_tl { I~saw~'#1'. \\ }
```

we get

> I saw 'stuff'. I saw 'which'. I saw 'i'. I saw 's'. I saw 'complicated'.

So you’ll see that spaces are ignored by the mapping, and that a brace group counts as a single item. I’ve not covered every token list and token list variable function, but hopefully the basic concepts are now laid out. In the next post, I’ll move on to some other concepts, so that we can being to put more structures together.
