---
layout: post
published: true
title: Wort chiller pump
mathjax: true
comments: true
share: true
chart: true
description: "and the art of over-engineering"
categories: 
  - Brewing
---

At the new apartment, my brewing has gone outdoors to the back patio. The patio drains off onto the cars parked below the patio, so running an open loop of water through my wort chiller isn't an option anymore. Not even to mention the ethics of dumping gallons of water during a drought.

I went looking around for a submersible aquarium pump to run a closed-loop water cycle in a cooler -- like the one shown in this image i jacked from some dude on flickr...

![wort chiller pumping](/image/post/2115697301_ff9c9a3de1.jpg)

Of course I became curious about how effective the cooling would be with different volumes of ice water. In a really simplified sense, the hot wort and cold bath can be treated as coupled isothermal baths with one inlet/outlet of fluid. The equations are

$$
\begin{equation}
m_b \cfrac{\mathrm{d}T_b}{\mathrm{dt}} = \dot{m}(T_i-T_b)\\\
m_c \cfrac{\mathrm{d}T_c}{\mathrm{dt}} = \dot{m}(T_b-T_i)\\\
\end{equation}
$$

where I'm calling $T_b$ the wort temperature and $T_c$ the cold bath temperature, $\dot{m}$ is the mass flow pushed by the pump, and $m_b$ and $m_c$ are the masses of fluid sitting in the hot and cold baths, respectively. I'll solve this by putting it into matrix form,

$$
\begin{equation}
\cfrac{\mathrm{d}}{\mathrm{dt}}\begin{bmatrix}T_b\\T_c\end{bmatrix} = \begin{bmatrix}-\alpha_b & \alpha_c \\ \alpha_c & -\alpha_c\end{bmatrix}\begin{bmatrix}T_b\\T_c\end{bmatrix}
$$