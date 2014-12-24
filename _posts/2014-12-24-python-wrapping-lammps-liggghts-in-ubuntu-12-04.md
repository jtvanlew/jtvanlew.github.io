---
layout: post
published: true
title: Python wrapping LAMMPS/LIGGGHTS in Ubuntu 12.04
mathjax: false
comments: true
share: true
chart: true
tags: lammps liggghts python DEM
categories: 
  - engineering
modified: "2014-12-24"
---

Update: I reformatted a computer in my lab with Ubuntu 14.04. I went through installing LIGGGHTS and the Python wrapper -- along with an mpi4py instead of pypar for parallelizing with Python. It was actually much simpler than the process I've outlined here. I'm going to leave this here for anyone with Ubuntu 12.04 but I want to note that if you've got a newer version of Ubuntu to ignore much of this...

<div id="wrapper" style="width:100%; text-align:center">
    <img src="http://lammps.sandia.gov/movies/logo.gif" alt="LAMMPS logo" />
</div>
<br />

As I've [discussed before](http://jon.vanlew.net/tag/liggghts.html), I've been using LIGGGHTS for my DEM simulations in my research. Whenever I've had to customize the program, I gotten around coding of the source (written in C++) by making use of the LAMMPS functionality of a [Python wrapper](http://lammps.sandia.gov/doc/Section_python.html). With that, instead of directly calling LIGGGHTS with input files, I have Python scripts that generate my input scripts as well as providing the convenience of all kinds of sophisticated Python hacking on top.

The first time I got it working on my (Ubuntu 12.04) machine at work, it took like a week of pulling out my hair on internet forums and just plain guess work. My hard drive on that computer failed recently so I had to get everything back up and running from scratch. Now I'm just slightly more savvy with the guts of Ubuntu so instead of a miserable week it was just an annoying afternoon. Feeling proud of myself, I figured I'd write this to help anyone else who might want the Python wrapper with Ubuntu -- as well as for future-me when I've got more computer problems and need to do this again.

Let's start from the very first step of pulling LIGGGHTS from the public git repository. You can get it here:
    git clone https://github.com/CFDEMproject/LIGGGHTS-PUBLIC.git ~/LIGGGHTS/LIGGGHTS-PUBLIC

If you don't have `mpic++` installed already, you'll need it to build LIGGGHTS. You should do an `apt-get`, it's 

    sudo apt-get install mpic++

Yours might be different and my expertise ends right there. With openmpi install, do a

    cd ~/LIGGGHTS/LIGGGHTS-PUBLIC/src

to get to the source directory. On Ubuntu 12.04, you can straight away do 

	make clean-all
	make fedora

This should take a while. If there are errors really look at the error log. Almost always there is some line in the log that tells you exactly what went wrong and where. It's often hidden among pages and pages of junk that's frightening and confusing to people like me. But keep looking and you'll find out exactly what you need (sometimes it's something like gfortran not being present).

All of that simply got your Ubuntu running with LIGGGHTS. Now we can get the Python wrapper working. This part is my contribution. from the source directory, navigate to the Make directory.

	cd ~/LIGGGHTS/LIGGGHTS-PUBLIC/src/MAKE

In there, locate the file named `Makefile.fedora`. Either do a `vim` to open it or `gedit`. Locate the line that says `shflag` (in mine it is line 11) and make it say

	shflag = -fPIC

Now save the file, close it and change back to LIGGGHTS src directory

	cd ..

You can create the library now that LAMMPS/LIGGGHTS needs for giving access to Python.

	make makeshlib
	make -f Makefile.shlib fedora

This might even take longer than the previous `make fedora` command. But once it's done you'll have a file named `liblammps_fedora.so` and `liblammps.so`. These will be used by Python. So to allow Python access, we need to inform the machine where they're located. With Ubuntu you can open your `.bashrc` file in your home directory and add the following two lines

	export PYTHONPATH=$PYTHONPATH:/home/jon/LIGGGHTS/LIGGGHTS-PUBLIC/python
	export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jon/LIGGGHTS/LIGGGHTS-PUBLIC/src

Note that my username is `jon` on that machine so you'll obviously need to replace that with your user.

You now should be able to open python in the terminal and then test LAMMPS with a 

	import lammps

command. Cross your fingers and hope that works. As a bonus, the way it's set up here, you can also download `pypar`, install it, and run LAMMPS in parallel with Python! I'm not 100% confident on the steps I used to get pypar running (though I'm _certain_ I have to make sure `openmpi1.5-bin` is used) so I don't want to give a walkthrough for that.

I hope this comes in handy for anyone else looking to use Python to avoid any of the miserable C++ coding of the source of LAMMPS/LIGGGHTS. Happy coding!

Update: I just went through the process on another computer at work and found the packages listed in the `pypar` readme were really all that were necessary to get it going if you've successfully done everything else above here. WITH TH EXCEPTION of needing specifically `openmpi1.5-bin`. These are the only packages you'd need:

	sudo apt-get install openmpi1.5-bin libopenmpi-dev python-dev python-numpy