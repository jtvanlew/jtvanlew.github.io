---
layout: post
published: true
title: Pebble breaking in DEM pt. 2
mathjax: false
comments: true
share: true
chart: true
categories: 
  - engineering
tags: "DEM liggghts Python"
---

The pebble breakage routine (introduced [Pebble breaking in DEM](/engineering/pebble-breaking-in-dem)) has received an upgrade but is still not complete. I've applied it here to a simulation of an oedemetric compression that we often do experimentally in the lab. There's still not a lot of thought going into the criteria that decides if a pebble breaks, each pebble just has to have a contact force greater than some pre-assigned weibull distribution of 'critical force'. But each broken pebble is replaced with a series of smaller particles with a gaussian distribution of their radii.

<iframe width="560" height="315" src="//www.youtube.com/embed/kBQb5AIC2Lo?list=UUrg_gFEwT_yt8oOLrAY6pJA" frameborder="0" allowfullscreen></iframe>

The next step is to mature the failure criteria based on some single pebble crushing experiments (which we can do in the lab), then run some more complete oedemetric simulations (with the total number of pebbles closer approaching reality), and try to match pebble bed simulations to the experiments. Once I get a little confidence with experimental validation, I'll start doing the much more simulation-time expensive thermal simulations with pebble failure.