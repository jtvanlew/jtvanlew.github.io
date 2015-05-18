---
layout: post
published: true
title: "LaTeX package: siunitx"
mathjax: true
comments: true
share: true
description: clever unit and number typesetting for latex
headline: "LaTeX package: siunitx"
categories: 
  - engineering
tags: "latex, siunitx, typesetting"
---

The first time I saw anyone mention the `siunitx` package for $\latex$ on the tex stackexchange was for formatting and alignment of different size numbers in tables. For example, if I had a column in a table with numbers like 1092.22 and 0.4 and 100, the default centering (or left or right) doesn't give any impression of the comparitive magnitude of the values unless they had the exact same number of digits. It was suggested to use the siunitx package so that all the values are aligned about the decimal point and then, at a glance, you could see the relative magnitudes of the numbers.

I looked at the documentation too briefly to understand its usefulness but also began using it for typesetting units on numbers. But I was doing it so hacky that I may as well have been not using it at all. I was doing things like,

{% highlight latex %}
... the effective heat transfer coefficient is calculated as 1.2~\si{W/m^2-K} ...
{% endhighlight %}

I didn't see any benefit to what was spit out in my pdf but for some reason kept enclosing my units with the `\si` command. Finally today I looked through the documentation again and discovered how much more useful and powerful siunitx really is. What I should have been doing with the above sentence is this

{% highlight latex %}
... the effective heat transfer coefficient is calculated as \SI{1.2}{\watt\per\square\meter\per\kelvin} ...
{% endhighlight %}

which might look uglier and like more work up front, what it does is powerful. Generally speaking, I am always publishing in American or American-styled European journals. So when I typeset units I rarely think about how other parts of the world don't follow the common American notation, e.g. period for the decimal point and commas for separating groups of 000 in large numbers. Or that I might be used to $W/m^2K$ but some journals might require it to be formatted as $W~m^{-2}~K^{-1}$, for instance.

When typesetting like in the latter example with siunitx package, it becomes simply a matter of changing the formatting parameter once and all units defined in the paper stay consistent and follow the guidelines you're aiming for. In that respect, it's a great package that is now a standard in the preamble of any of my $\latex$ papers.