---
title: "Hello dark mode, my old friend...I've come to need you yet again."
description: "Dark mode for fastpages"
layout: post
toc: false
comments: true
image: images/chart-preview.png
hide: false
search_exclude: true
categories: [fastpages, jupyter]
---


This time for my `fastpages` blog.

I have not dabbled in designing dark mode experiences before and therefore, plan to keep this process simple and understandable. Any feedback on improving the experience is obviously appreciated.

I also need not explain to you the benefits of having dark mode enabled unless you masochistically enjoy straining your eyes with bright light. For someone who spends a good part of the day stuck behind a screen, I'd like to optimize the viewing experience.

Now onward!

We shall being using a bunch of simple css rules while (mostly) following Material Design guidelines. 

Here's the fastpage sample blog post without Dark mode.

![]({{ site.baseurl }}/images/light-mode.png)

And here's the one with dark mode enabled!

![]({{ site.baseurl }}/images/dark-mode.png)

Pretty cool, yeah? 

Now onto the code. If you're in a hurry to join the dark side, feel free jump to this section and copy-paste the CSS rules into the custom stylin section of your blog.

If your curious about the design choices I've made and would like to customise for yourself, stick with me here.

The stylesheet is actually pretty straightforward.

```scss
$high-emph: rgba(white, 0.87);
$med-emph: rgba(white, 0.69); //Noicee
$low-emph: rgba(white, 0.38);
$dark-grey : #121212;
$overlay: mix($dark-grey, white, 95%);
$overlay-light: mix($dark-grey, white, 86%);
```

We use a very simple colour palette. 

- 3 shades of white for different levels of emphasis of text
- Base dark colour which is recommended by Material design and its lighter shages for components such as codeblocks and tables

Feel free to experiment with theme colours and accents but the defaults are more or less visually very appealing. (Trust me, I've already obsessed over this)

# Show me the money

Feel free to experiment with theme colours and accents but the defaults are more or less visually very appealing. (Trust me, I've already obsessed over this)
