.. _Session4:

************************************************************************************
Session 4. Making initial condition files and compile
************************************************************************************

1. Overview
======================================================

For each physics problem that you want to study using AREPO, you need to have several files in your stage directory where you run simulations.

1. Initial condition file (``*.hdf5``): This file describes the initial state of the system that you are interested in
2. Parameter file (``param.txt``): This file contains the values of parameters needed to simulate the system.
3. Configuration file (``Config.sh``): This file contains necessary configurations.
4. Additional files: this files include those that are specific to the problems, such as a file contatining a pre-tabulated table for Helmholtz equation of state.

``Config.sh`` is the only file you need to compile the code. To run the code, you need the initial condition file, parameter file, and additional files (if necessary). From now on, all the files (``*.hdf5``, ``param.txt``, ``Config.sh``) will be collectively denoted as ''initial setup files``.

This session comprises of two sub-sessions. In the first sub-session (``1. Make initial setup files``), we will make all those initial condition files and in the second sub-session (``2. Compilation``), we will compile the code.


1. Make initial setup files
======================================================

For some hydrodynamics codes, a file that creates the initial setup for a simulation is compiled together with the main part of the code. In this method, the code generates the initial conditions of the system once the simulation runs.  However, ``AREPO`` takes another approach in which making initial condition files and running the simulation are separated. So users make the initial condition files before running simulations, and once you start the simulation, the code reads the initial condition files and maps the initial setup (e.g., domain size, mass distribution, and so on) into the domian, and evolves the system. Two ways that I found convenient when it comes to creating initial condition files and running simulations using AREPO are,

1. create initial condition files and run the simulation in one directory (Session 6. Practice 1 - shock-tube): I would recommend this approach if you plan to run only a few simulations.

2. create initial condition files in one directory and run the simulation in a separate directory (Session 7. Practice 2 - relaxation of main-sequence star): I would recommend this if you plan to run many simulations (more than a few) with similar setups (e.g., 5 simulations for collisions between 1Msol stars, 5 simulations for 2Msol stars, 5 simulations for 10 Msol stars). For that case, it would be more convenient not only to write a python script which creates the initial conditions, but also puts them in a stage directory for each simulation.

Of course, these are not the only ways. Users can develope their own workflow.

We will proceed this tutorial using the shock tube test as the first exercise, which is located in ``<AREPO_directory>/run/Shock_tube``. A python script for generating the initial condition file (``create.py``), a sample parameter file, and a configuration file (Config.sh) are already included in the directory.

1) Create initial condition file
---------------------------------

2) Create parameter file
-------------------------

3) Create configuration file
-----------------------------



2. Compilation
======================================================
Let's do the part that first-time users spend a long time on. As before, we will go through this step by step.

1) Load modules
---------------

We need several modules to compile and run AREPO. Let's load the following modules,

.. code-block:: console

   $ source /usr/common/appl/modules-tcl/init/sh
   $ module purge
   $ module load mpich/3.3.6
   $ module load fftw-mpich/3.3.6
   $ module load gsl
   $ module load hdf5/1.8.18

2) Set SYSTYPE
------------------

To successfully compile almost every hydrodynamics code, it is very important to set the paths to the dependences (e.g., those modules we just loaded) inside the code. As mentioned above, because the paths to the modules are different for dffierent machines, you have to set the paths for each machine you are using. Every code has a different file in which you need to set the paths. The file for ``AREPO`` is ``makefiles/systypes.make``. Fortunately, the system setup for the mpa cluster, raven, cobra, and freya were already set! All you need to do is to make sure that you tell the code correctly which system you are on. You can set the system type by,

.. code-block:: console

   $ export SYSTYPE=pascal

One convenient way is to add the line to your bash file (``~/.bashrc``) and do ``source ~/.bashrc`` instead of typing the line above.


3) Compile
---------------

We need a test case for which compile the code. To compile, you first go to the ``AREPO`` directory,

.. code-block:: console

   $ cd /afs/mpa/temp/<path_to_your_directory>/AREPO/


3. Restart
======================================================



A few tips that are good to know.

1. The AREPO domain with box size `L` starts from 0 to `L`, not `-L/2` to `L/2`. So you need to re-adjust the domain origin when you make an initial condition file.

2. To comment out in the parameter file, use ``%``. However, use ``#`` to comment out in the configuration file.
