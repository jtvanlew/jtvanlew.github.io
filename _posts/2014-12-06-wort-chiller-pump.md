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

![wort chiller pumping](/images/post/2115697301_ff9c9a3de1.jpg)

Of course I became curious about how effective the cooling would be with different volumes of ice water. In a really simplified sense, the hot wort and cold bath can be treated as coupled isothermal baths with one inlet/outlet of fluid. I'll assume also that the wort chiller I made is efficient enough to raise the temperature of the chilling water up to the wort  temperature, regardless of the flow rate or chilled temperature. The equations are

$$
\begin{equation}
m_b \cfrac{\mathrm{d}T_b}{\mathrm{dt}} = \dot{m}(T_i-T_b)\\\
m_c \cfrac{\mathrm{d}T_c}{\mathrm{dt}} = \dot{m}(T_b-T_i)\\\
\end{equation}
$$

where I'm calling $T_b$ the wort temperature and $T_c$ the cold bath temperature, $\dot{m}$ is the mass flow pushed by the pump, and $m_b$ and $m_c$ are the masses of fluid sitting in the hot and cold baths, respectively. I'll solve this by putting it into matrix form,

$$
\begin{equation}
\cfrac{\mathrm{d}}{\mathrm{dt}}\begin{bmatrix}T_b\\T_c\end{bmatrix} = \begin{bmatrix}-\alpha_b & \alpha_b \\ \alpha_c & -\alpha_c\end{bmatrix}\begin{bmatrix}T_b\\T_c\end{bmatrix}
\end{equation}
$$

The vector-form of the simple ODE is solved in the same form as any other ODE. Good detail can be found [on this site](http://tutorial.math.lamar.edu/Classes/DE/SolutionsToSystems.aspx). To find the solution, we'll find the eigen values from the determinant of the coefficient matrix. The two eigen values are $\lambda_1 = 0$ and $\lambda_2 = -(\alpha_b + \alpha_c)$. The corresponding eigen vectors are

$$\bar{\eta}_1 = \begin{bmatrix}1\\1\end{bmatrix}$$

and 

$$\bar{\eta}_2 = \begin{bmatrix}1\\-\alpha_c/\alpha_b\end{bmatrix}$$ 

where $\alpha_b = \dot{m}/m_b$ and $\alpha_c = \dot{m}/m_c$. Thus the general solution is

$$
\begin{equation}
\begin{bmatrix}T_b\\T_c\end{bmatrix} = C_1\begin{bmatrix}1 \\ 1 \end{bmatrix} + C_2 e^{-(\alpha_c + \alpha_b)t}\begin{bmatrix}1\\-\alpha_c/\alpha_b\end{bmatrix}
\end{equation}
$$

The initial conditions can be just taken as boiling for the hot bath and freezing for the cold one, $T_{b,i} = 212$ F and $T_{c,i} = 32$ F. The coefficients are then

$$
\begin{equation}
C_1 = T_{b,i} - \cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}\\\
C_2 = \cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}
\end{equation}
$$

Finally, the solutions, when broken out of vector form, are

$$
\begin{equation}
T_b(t) = T_{b,i} + \left[e^{-(\alpha_b+\alpha_c)t}-1\right] \left(\cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}\right)\\\
T_c(t) = T_{b,i} + \left[-\left(\alpha_c/\alpha_b\right)e^{-(\alpha_b+\alpha_c)t}-1\right] \left(\cfrac{T_{b,i} - T_{c,i}}{1+\alpha_c/\alpha_b}\right)
\end{equation}
$$

I found a pump on Amazon that was $7 and ran at 80 gal/hr. I'll assume that my wort is about 3 gallons. So I want to compare the temperatures of the two baths as the cold bath volume changes. Like, can 3 gal of frozen water drop 3 gal of boiling water to 80 F? (no) or what size do I need in order to actually hit 80 F? The easiest way to solve this is with some simple scripting.

The code is given in its entirety at the bottom. The plot coming from the code is:

![wort chiller temp plots](/images/post/figure_2.png)

The upper lines are the plots of hot water bath temperatures with time, starting with 1 gal, then going 3, 6, 9, 12, and 15 gallons for the cold bath. The lower, dashed lines are the cold baths for the same cold bath volumes.

What the lines show us is that for cold water baths less than 9 gal we'll never hit 80 F before the thermal energy equilibrates between the two water volumes. At 9 gal and above, however, we hit 80 F at earlier times for larger the volumes.

I wrapped up the equations in some pert little code, reproduced here for prosperity
{% highlight py %}
import numpy as np
import matplotlib.pyplot as plt

def KtoF(T):
	return (T-273)*1.8+32

def StoM(t):
	return t/60

Q = 80 * 0.00105150 # gal/hr to L/s
rho = 1000     		# water density 
Vb = 3*.00379  		# gal to m3 hot bath
Vcg = np.array([1, 3, 6, 9, 12])

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
	mc = rho*Vcg 	# mass of cold bath
	alphac = Q/mc

	gamma = (Tbi-Tii)/(1+alphac/alphab) # intermediate calc

	Tb = Tbi + (np.exp(-(alphab + alphac)*t)-1)*gamma
	Ti = Tbi + (-(alphac/alphab)*np.exp(-(alphab + alphac)*t)-1)*gamma
	plt.plot(StoM(t),KtoF(Tb))
	plt.plot(StoM(t),KtoF(Ti),
		label=str(v)+' gal',
		linestyle='--'
		)
plt.show()
{% endhighlight %}