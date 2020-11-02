---
title: "Hello dark mode, my old friend..."
description: "Dark mode theme for fastpages"
layout: post
toc: false
comments: true
image: images/dark-side.gif
hide: false
search_exclude: false
categories: [colours, jekyll, css, fastpages]
---


I have come to talk with you again, this time for my `fastpages` blog. 

`fastpages` gets a lot of things right for someone who uses `Jupyter` notebooks and wants to get into blogging. Prashanth Rao's [article](https://prrao87.github.io/blog/blogging-for-data-scientists/) does a great job of making the case for that.

# But why?

However, being a long time user of the [Dark Reader](https://darkreader.org/) browser extension, it was unusual to not have widespread dark mode support on many Jekyll themes, one of which `fastpages` is built on. Therefore, I decided to bring back the dark mode experience in this post.

![]({{ site.baseurl }}/images/dark-side.gif)

I personally prefer dark mode to light as it causes lesser strain on the eyes. It also helps illuminate content while the background fades away. For someone who spends a good part of the day stuck behind a screen, I've made it a point to keep the bright light intake for outdoors.

Since I have not dabbled in designing dark mode experiences before, I plan to keep this process simple and understandable. We shall be using a bunch of simple css rules while following Material Design dark theme [guidelines](https://material.io/design/color/dark-theme.html) (mostly).

Here's the sample fastpages sample blog [post](https://fastpages.fast.ai/jupyter/2020/02/20/test.html) without Dark mode: 

![]({{ site.baseurl }}/images/light-mode.png "Curb your light mode")

And here's the [same one](http://prudhvirampey.com/new_blog/jupyter/2020/02/20/test.html) with dark mode enabled!

![]({{ site.baseurl }}/images/dark-mode.png)

Pretty cool, yeah? Let's check out the code now.

If you're in a hurry to join the dark side, feel free to scroll to the end of this post and download the dark mode stylesheet.

If your curious about the design choices I've made and would like to customize for yourself, stick with me here.

# Colour palette

Let's start with defining our palette.

```scss
$high-emph: rgba(white, 0.87); // Colour 1 -> White
$med-emph: rgba(white, 0.69); //Noice
$low-emph: rgba(white, 0.38);
$dark-grey : #121212; // Colour 2
$overlay: mix($dark-grey, white, 95%);
$overlay-light: mix($dark-grey, white, 86%);
```

That's it. Two colours and their shades.

![]({{ site.baseurl }}/images/palette.svg "From left, dark grey and its shades and then the whites")

- Baseline `dark-grey` theme colour which is recommended by Material design and *lighter* variants of it for components such as code blocks and tables.
- Shades of `white` for different levels of emphasis of text. [^1]

This also gives us the flexibility to choose *our own* primary dark color. For eg, if we change the value of `dark-grey` to that of something like `deep-purple` (`#1F1B24`). Voilà, we get the following palette:

![]({{ site.baseurl }}/images/palette-2.svg)

and theme:

![]({{ site.baseurl }}/images/purple-mode.png)

The palette can be easily customized to support your own favorite dark colour!

# The little things that matter

The rest of the stylesheet is more or less straightforward. Here are some additional quirks that I thought were cool:

- Don't forget to turn over your faithful scrollbar to the dark side  
  
```scss
* {
    scrollbar-color: $dark-grey $overlay-light;
}
```


![]({{ site.baseurl }}/images/scrollbars.png)


- You can invert the colour of your charts and plots to keep that dark consistency going.  
  
```scss
canvas {
    filter: invert(100%);
}
```

![]({{ site.baseurl }}/images/light-dark-viz.png "I like my graphs like I like my chocolate, dark")

> Psst, Check out the dark graphs in action [here](http://prudhvirampey.com/new_blog/jupyter/2020/02/20/test.html#Example-1:-DropDown).


- We also got some dark tables in the house babyy 👾

```scss
table th {
    background-color: $overlay;
    border-color: $overlay-light;
    color: $high-emph;
}

table td {
    background-color: $dark-grey;
    border-color: $overlay-light;
    color: $med-emph;
}
```

![]({{ site.baseurl }}/images/light-dark-tables.png "Let there be shiny data")


# Show me the money (code)

You can get the stylesheet from this Github gist [here](https://gist.github.com/prampey/aac8f8436827ea09f53a67873142706c). Save it to `_sass/minima` and add this import line in `custom-styles.scss`.

```scss
/*-----------------------------------*/
/*----- ADD YOUR STYLES BELOW -------*/

@import "minima/dark-mode";
```

That's it! `fastpages` finally has the power of the dark side.

Enjoy ⚡

# Footnotes

[^1]: More on maintaining text legibility while deciding colour [here](https://material.io/design/color/text-legibility.html#legibility-standards)
