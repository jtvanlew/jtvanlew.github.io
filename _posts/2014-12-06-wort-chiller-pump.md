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
tags: "wort chiller, homebrewing, pump"
---

At the new apartment, my brewing has gone outdoors to the back patio. The patio drains off onto the cars parked below the patio, so running an open loop of water through my wort chiller isn't an option anymore. Not even to mention the ethics of dumping gallons of water during a drought.

I went looking around for a submersible aquarium pump to run a closed-loop water cycle in a cooler -- like the one shown in this image i jacked from some dude on flickr...

![wort chiller pumping](/images/post/2115697301_ff9c9a3de1.jpg)

Of course I became curious about solving the energy balance for the temperatures of the wort as a function of time. It becomes interesting when you consider that the cold water flushes through the hot wort, and then warms up the cold bath as it dumps back into the reservoir. The curiosity is mostly academic and not really influencing a design as I see it. But ... here goes.

# Equations
In a really simplified sense, the hot wort and cold bath can be treated as coupled isothermal baths with one inlet/outlet of fluid. A schematic of the exchange is here:

![wort chiller schematic](/images/post/wort_chiller.png)

For this problem the cold fluid is all at $T_c$ whether its in the bath or in the transfer line. Same goes for the hot wort and hot end of the transfer line. Doing any open, transient energy balance on the two baths yields the simple coupled system of ODEs:

$$
\begin{equation}
m_b \cfrac{\mathrm{d}T_b}{\mathrm{dt}} = \dot{m}(T_c-T_b)\\\
m_c \cfrac{\mathrm{d}T_c}{\mathrm{dt}} = \dot{m}(T_b-T_c)\\\
\end{equation}
$$

Obviously $\dot{m}$ is the mass flow pushed by the pump, and $m_b$ and $m_c$ are the masses of fluid sitting in the hot and cold baths, respectively. I'll solve this by putting it into matrix form,

$$
\begin{equation}
\cfrac{\mathrm{d}}{\mathrm{dt}}\begin{bmatrix}T_b\\T_c\end{bmatrix} = \begin{bmatrix}-\dot{m}/m_b & \dot{m}/m_b \\ \dot{m}/m_c & -\dot{m}/m_c\end{bmatrix}\begin{bmatrix}T_b\\T_c\end{bmatrix}
\end{equation}
$$

The vector-form of the simple ODE is solved in the same method as we would a classical first order ODE. Good detail can be found [on this site](http://tutorial.math.lamar.edu/Classes/DE/SolutionsToSystems.aspx). In other words, we can assume the solution is of some form (exponential) and then where the time constant in the exponential growth/decay comes from eigenvalues of the problem. For this system of equations, we find not only the eigenvalues but eigenvectors.

The two eigenvalues are $\lambda_1 = 0$ and $\lambda_2 = -(\dot{m}/m_b + \dot{m}/m_c)$. The corresponding eigen vectors are

$$\bar{\eta}_1 = \begin{bmatrix}1\\1\end{bmatrix}$$

and 

$$\bar{\eta}_2 = \begin{bmatrix}1\\-m_b/m_c\end{bmatrix}$$ 

Thus the general solution is

$$
\begin{equation}
\begin{bmatrix}T_b\\T_c\end{bmatrix} = C_1\begin{bmatrix}1 \\ 1 \end{bmatrix} + C_2 e^{-(\dot{m}/m_b + \dot{m}/m_c)t}\begin{bmatrix}1\\-m_b/m_c\end{bmatrix}
\end{equation}
$$

The initial conditions are left as just generic values for both baths. Plugging in those values at time $t=0$ to the general solution let's us find the coefficients:

$$
\begin{equation}
C_1 = T_{b,i} - \cfrac{\Delta T_i}{1+m_b/m_c}\\\
C_2 = \cfrac{T_{b,i} - T_{c,i}}{1+m_b/m_c}
\end{equation}
$$

where $\Delta T_i$ is just the difference in temperatures of the two baths at the initial condition. I'll define the ratio of hot-cold baths as a dimensionless parameter $\alpha$. When $\alpha < 1$, the hot bath is being cooled by a larger mass of cold water. Vice versa for $\alpha > 1$. 

Finally, the solutions, when broken out of vector form, are

$$
\begin{equation}
T_b(t) = T_{b,i} - \left(\cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}\right)\left[1-e^{-\dot{m}/m_b(1+\alpha)t}\right] \\\
T_c(t) = T_{b,i} - \left(\cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}\right)\left[1+\left(\frac{m_b}{m_c}\right)e^{-\dot{m}/m_b(1+\alpha)t}\right] 
\end{equation}
$$

## Result
I found a pump on Amazon that was $7 and ran at 80 gal/hr. I'll assume that my wort is about 3 gallons. So I want to compare the temperatures of the two baths as the cold bath volume changes. Like, can 3 gal of frozen water drop 3 gal of boiling water to 80 F? (no) or what size do I need in order to actually hit 80 F? The easiest way to solve this is with some simple scripting.

The code is given in its entirety at the bottom. The plot coming from the code is:

![wort chiller temp plots](/images/post/figure_2.png)

The upper lines are the plots of hot water bath temperatures with time, starting with 1 gal, then going 3, 6, 9, 12, and 15 gallons for the cold bath. The lower, dashed lines are the cold baths for the same cold bath volumes.

What the lines show us is that for cold water baths less than 9 gal we'll never hit 80 F before the thermal energy equilibrates between the two water volumes. At 9 gal and above, however, we logically hit 80 F earlier with larger cold volumes.

If I do it again with a flowrate of $Q = 158$ gph, 

![wort chiller temp plots](/images/post/pump-q158.png)

All that happens is a faster approach to steady state temperature, but it doesn't do anything for the actual steady state value. A careful inspection of Eqs. (5) should have revealed that before we began. But I'm nothing if not careful. Pretty cool though, the biggest determining factor (if a few minutes of time isn't critical) is simply the volume of cold water bath.

Now... what does that have anything to do with buying a pump? Well, not much. The difference between an 80 gph pump and a 158 gph pump (at twice the price) would be hitting pitching temperatures faster -- but even the slow pump can do it. But it does tell me an important result that if I'm running a closed-loop wort chiller, I'd better be prepared with a much larger volume of cold water than hot water I need to chill. 

I think, perhaps, most importantly this demonstrated that I really need to get outside more often.

## Code
I wrapped up the equations in some pert little code, reproduced here for posterity
{% highlight py %}
import numpy as np
import matplotlib.pyplot as plt

def KtoF(T):
	return (T-273)*1.8+32

def StoM(t):
	return t/60
Qgph = 158
Q = Qgph * 0.00105150 # gal/hr to L/s
rho = 1000     		# water density 
Vb = 3*.00379  		# gal to m3 hot bath
Vcg = np.array([1, 3, 6, 9, 12, 15])

mb = rho*Vb  		# mass of the wort
alphab = Q/mb

t = np.linspace(0,500,100)
Tmin = np.zeros(len(t))+80
Tii = 273 			# K
Tbi = 373 			# K

plt.close('all')
plt.plot(StoM(t),Tmin,'k',linewidth=3,label='80 F limit')
plt.xlim([0,StoM(t[-1])])
plt.xlabel('Time (minutes)')
plt.ylabel("Temperature (F)")
plt.grid()

# looping over different cold water bath volumes
for v in Vcg:
	Vc = v*.00379	# cold bath volume (m3)
	mc = rho*Vc 	# mass of cold bath
	alphac = Q/mc

	gamma = (Tbi-Tii)/(1+alphac/alphab) # intermediate calc

	Tb = Tbi + (np.exp(-(alphab + alphac)*t)-1)*gamma
	Ti = Tbi + (-(alphac/alphab)*np.exp(-(alphab + alphac)*t)-1)*gamma
	plt.plot(StoM(t),KtoF(Tb), label=str(v)+' gal cold')
	plt.plot(StoM(t),KtoF(Ti), 'k--')
plt.legend(loc='best', ncol=2)
plt.title('Pump flowrate %s gph'%(Qgph))
plt.show()
{% endhighlight %}