.. _Session4:

************************************************************************************
Session 4. Making initial condition files and compile
************************************************************************************

1. Overview
======================================================

For each physics problem that you want to study using AREPO, we need to have several files in your stage directory where you run simulations.

1. Initial condition file (``*.hdf5``): This file describes the initial state of the system that you are interested in
2. Parameter file (``param.txt``): This file contains the values of parameters needed to simulate the system.
3. Configuration file (``Config.sh``): This file contains necessary configurations, which will be used to compile the code.
4. Additional files: this files include those that are specific to the problems, such as a file contatining a pre-tabulated table for Helmholtz equation of state.

This session comprises of two sub-sessions. In the first sub-session (``1. Make initial condition files``), we will make all those initial condition files and in the second sub-session (``2. Compilation``), we will compile the code.


1. Make initial condition files
======================================================

For some hydrodynamics codes, a file that creates the initial setup for a simulation is compiled together with the main part of the code. However, ``AREPO`` takes another way in which the initial condition files are made separately before running simulations and once you run the code, the code reads the initial condition files and generates the initial setup (e.g., domain size, mass distribution, and so on) in the domian. So for users, there are mainly two ways to proceed,

1. create initial condition files and run simulations in one directory (Session 6. Practice 1 - shock-tube): I would recommend this approach if you plan to run only a few simulations.

2. create initial condition files in one directory and run simulations in separate directories (Session 7. Practice 2 - relaxation of main-sequence star): I would recommend this if you plan to run many simulations (more than a few) with similar setups (e.g., 5 simulations for collisions between 1Msol stars, 5 simulations for 2Msol stars, 5 simulations for 10 Msol stars). For that case, it would be more convenient for you to write a python script which creates the initial conditions and put them in a stage directory for different simulations.

We will prepare the initial conditions for the shock tube test as the first exercise.

2. Compilation
======================================================
Let's do the part that first-time users spend a long time on. As before, we will go through this step by step.

1. Load modules
---------------

We need several modules to compile and run AREPO. Let's load the following modules,

.. code-block:: console

   $ source /usr/common/appl/modules-tcl/init/sh
   $ module purge
   $ module load mpich/3.3.6
   $ module load fftw-mpich/3.3.6
   $ module load gsl
   $ module load hdf5/1.8.18

2. Set SYSTYPE
------------------

To successfully compile almost every hydrodynamics code, it is very important to set the paths to the dependences (e.g., those modules we just loaded) inside the code. As mentioned above, because the paths to the modules are different for dffierent machines, you have to set the paths for each machine you are using. Every code has a different file in which you need to set the paths. The file for ``AREPO`` is ``makefiles/systypes.make``. Fortunately, the system setup for the mpa cluster, raven, cobra, and freya were already set! All you need to do is to make sure that you tell the code correctly which system you are on. You can set the system type by,

.. code-block:: console

   $ export SYSTYPE=pascal

One convenient way is to add the line to your bash file (``~/.bashrc``) and do ``source ~/.bashrc`` instead of typing the line above.


3. Compile
---------------

We need a test case for which compile the code. To compile, you first go to the ``AREPO`` directory,

.. code-block:: console

   $ cd /afs/mpa/temp/<path_to_your_directory>/AREPO/


3. Restart
======================================================
