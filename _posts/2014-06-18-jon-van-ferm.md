---
layout: post
title: The VLFerm Part 1 -  Energy balance
slug: jon-van-ferm
tags: homebrew
category: Brewing
author: JVL
lang: en
mathjax: true
comments: true
share: true
chart: true
---
<div id="wrapper" style="width:100%; text-align:center">
    <img src="http://jon.vanlew.net/images/jon-van-ferm.jpg" alt="picture of the fermenter being tested" />
</div>
<br />

I saw this immersion chiller for fermenters on kickstarter a while back, the [BrewJacket Immersion](https://www.kickstarter.com/projects/433436998/brewjacket-immersion-lager-beer-without-a-refriger). I think it's actually an excellent solution to the problem of fermenting with not enough space for a dedicated fridge -- but wanting to control temperatures. The problem for me is that they want a $300+ donation in order to get your hands on one. Well, hell, why don't we find out the kinds of heat removal rates they're getting and see if I can't hack one together on my own?

If you look at the info for the BrewJacket Immersion chiller, you see

> Immersion can bring your beer down to 35º F below ambient in a matter of days and hold it there for as long as it is plugged into the wall.

For something to take that long to bring a bucket of beer down to some temperature, it can't be pulling out too many Watts. Let's just assume that the BrewJacket part of the Immersion chiller is providing a completely adiabatic boundary to the walls of the bucket (i.e. the only path heat can leave/enter is through the chiller). So every Joule of energy you pull from the system works to simply drop the temperature. In this system we can simply do a little volumetric energy balance,

$$
\begin{equation}
\rho c_p V \cfrac{\mathrm{d}T}{\mathrm{dt}} = Q_\text{out}
\end{equation}
$$

We can approximate the beer as just water, so we know the density, the specific heat, and of course the volume of liquid:

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

That's easy then. Even a simple peltier thermoelectric device can pull out 7 W. Of course, the walls of the fermenter won't be adiabatic. Even if we put in a little 3x design margin on this, a 21 W peltier isn't out of the question.

So here's how I imagined it. A bar of stainless (or aluminum) with an old cpu heat sink clamped on top of a peltier. The peltier gets fed a 20V power supply (via a relay) controlled by an arduino. The control comes from some temperature measurements (perhaps directly in the beer?). This, in theory, almost entirely matches the construction that the BrewJacket Immersion appears to have. 

I picked up some parts and began temp. testing the peltier on a bucket of water. So far my data is not beautiful (my power supply was giving a dirty voltage) so I'll stop here and submit another summary of construction and arduino code once things are working a little cleaner.

