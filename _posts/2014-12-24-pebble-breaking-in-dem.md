---
layout: post
published: true
title: Pebble breaking in DEM
mathjax: false
comments: true
share: true
chart: true
tags: "liggghts, DEM, python"
categories: 
  - engineering
modified: "2014-12-24"
---

The guts of my research for the last year or so has been on predicting the effects on the thermomechanics of a packed bed if there are individual pebbles in that bed that are cracking or breaking. This is important for fusion reactors because for the 'solid breeder' concept, we'd have packed beds of brittle ceramics that are doing the heat conversion and tritium generation. If something like the thermal conductivity (which is bad to begin with) begins to drop when pebbles break, we need to know that ahead of time.

<iframe width="560" height="315" src="//www.youtube.com/embed/xr_CfAC8nhA?list=UUrg_gFEwT_yt8oOLrAY6pJA" frameborder="0" allowfullscreen></iframe>

So the first generation model I made (with LIGGGHTS and LAMMPS doing the brunt of the work), just randomly selected pebbles as 'failed' and then removed them completely from the packed bed. This was crude, to be sure. So my next step (which was much more challenging) was not only predicting failure from inter-pebble forces (still not complete) but also converting a 'pebble' into 'fragments' with the code. I now have a pretty good structure for doing both tasks -- even if they're not ideal at the moment, they can be enhanced really simply when I do bring in physics and reality into the model.

Here's a sample of a test bed I made to check my code. I fill a cylindrical volume with pebbles that just give me something to shoot at. Then I create an atom that is shot at the bed -- attempting to break it. What you see is the pebble impacting the bed and instantly breaking itself and 2 other pebbles into a handful of smaller spherical fragments. The fragmentation process stops there because the tiny pebbles right now only conserve temperature, not momentum. Give it a peep on the youtube here...