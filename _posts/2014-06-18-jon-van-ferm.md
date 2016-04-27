---
layout: post
title: "The VL-Ferm Part 1"
description: energy balance
tags: 
  - homebrew
  - engineering
lang: en
mathjax: true
comments: true
share: true
chart: true
published: true
categories: 
  - brewing
---

<div id="wrapper" style="width:100%; text-align:center">
    <img src="http://jon.vanlew.net/images/jon-van-ferm.jpg" alt="picture of the fermenter being tested" />
</div>
<br />

The problem of tiny apartment space and controlled brewing is a problem I'm intimately familiar with here in LA as a grad student. Having naturally constant temperatures for two weeks *seems* like it wouldn't be a problem here but I always run into gigantic temperature swings whenever I throw the wort into the fermenter. My approach thus far has followed along these steps:

1. deal with it.

Which, while beautiful in its simplicity, doesn't always yield the most optimum deliciousness of beer. Then I saw a kickstarter for the [BrewJacket](http://www.brewjacket.com/). I found it to be a pretty simple solution that I could totally steal the design of. I know of some pretty low power peltier coolers that I hadn't ever considered being strong enough for keeping beer cool. I thought I would compare some of the stats given in the BrewJacket kickstarter to see how much power they must be removing with their device. On their page, it said

> Immersion can bring your beer down to 35º F below ambient in a matter of days and hold it there for as long as it is plugged into the wall.

For something to take that long to bring a bucket of beer down to some temperature, it can't be pulling out too many Watts. Let's just assume that the BrewJacket part of the Immersion chiller is providing a completely adiabatic boundary to the walls of the bucket (i.e. the only path heat can leave/enter is through the chiller). So every Joule of energy you pull from the system works to simply drop the temperature. In this system we can then simply do a little volumetric energy balance,

$$
\begin{equation}
\rho c_p V \cfrac{\mathrm{d}T}{\mathrm{dt}} = Q_\text{out}
\end{equation}
$$

Beer is predominately water, so we'll use its material properties:

$$
\begin{eqnarray}
\rho = 1000 ~\text{kg/m$^3$}\\\
c_p = 4179 ~\text{J/kg-K}\\\
v = 5 ~\text{gal} * 0.00379\cfrac{\text{m$^3$}}{\text{gal}} = 0.0189 \text{m$^3$}
\end{eqnarray}
$$

Now let's just say that the beer started at, maybe, 80º F and then fell down to 35º F in 3 days; so dT = 25 K and dt = $2.59\times 10^{5}$ s. This lets us find $Q_\text{out}$

$$
\begin{eqnarray}
Q_\text{out} & = & 1000 ~\text{kg/m$^3$} \times 4179 ~\text{J/kg-K} \times 0.0189 \text{m$^3$} \times 25~\text{K} / 2.59e5~\text{s}\\\
Q_\text{out} & = & 7 ~\text{J/s}
\end{eqnarray}
$$

Dude. 7 W? That's easy! But, yeah, you're right, the fermenter walls won't be adiabatic so let's add a design margin. Let's say we need 20 W of cooling. I think even cheap-o peltier thermoelectrics can pull 20 W. Since I had precisely such cheap-o peltier, I kinda hacked together some hardware with a flat bar of stainless, an old cpu heat sink, and a peltier sandwiched in the middle. My arduino + a relay got a 20 V power supply onto the thermoelectric. 

What you see in that image at the top is the first trial run of the whole assembly. I must admit it didn't work that well at first. There was too much stainless steel rod exposed and interacting with the room's air. Some insulation wrapped around that would force more energy interaction with the liquid it's immersed in.

Anyway. I've dubbed this monstrosity the VL-Ferm