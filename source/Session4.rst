.. _Session4:

************************************************************************************
Session 4. Making initial condition files and compilation
************************************************************************************

Overview
======================================================

To run ``AREPO`` simulations for a physics problem that you want to study, you need to have several files in your stage directory where you run the simulations.

- Initial condition file (``*.hdf5``): This file describes the initial state of the system, e.g., position, velocity, density, internal energy of each cell describing the system.
- Parameter file (``param.txt``): This file contains a list of parameters needed to simulate the system and their values.
- Configuration file (``Config.sh``): This file contains a list of configuration commands.
- Additional files: These include files specific to the problem, such as a file containing a pre-tabulated table for Helmholtz equation of state.

``Config.sh`` is the only file you need when compiling the code. To run the code, you need the initial condition file, parameter file, and additional files (if necessary). From now on, all the files (``*.hdf5``, ``param.txt``, ``Config.sh``) will be collectively denoted as ''initial setup files``.

This session comprises of two sub-sessions. In the first sub-session (``1. Make initial setup files``), we will make all those initial setup files and in the second sub-session (``2. Compilation``), we will compile the code.


Make initial setup files
======================================================

For some hydrodynamics codes, a file that creates the initial setup for a simulation is compiled together with the main part of the code. Then the code generates the initial conditions of the system once the simulation starts.  However, ``AREPO`` takes another approach in which making initial condition files and running the simulation are separate processes. So users make the initial condition files before running simulations, and once you start the simulation, the code simply reads the initial condition files you created and maps the initial setup (e.g., domain size, mass distribution, and so on) into the domain, and evolves the system. Two ways that I found convenient when it comes to creating initial condition files and running simulations using ``AREPO`` are,

1. create initial condition files and run the simulation in one directory (e.g., Sod's shock-tube): I would recommend this approach if you plan to run only a few simulations.

2. create initial condition files in one directory and run the simulation in a separate directory (Sessions 6 and 7. Practice 1-2): I would recommend this if you plan to run many simulations (more than a few) with similar setups (e.g., 5 simulations for collisions between 1Msol stars, 5 simulations for 2Msol stars, 5 simulations for 10 Msol stars). For that case, it would be more convenient for you to write a python script such that it not only creates the initial conditions, but also puts them in a stage directory for each simulation.

Of course, these are not the only ways. Users can develope their own workflow.

We will proceed this session using the shock tube test as the first exercise, which is located in ``<AREPO_directory>/run/Shock_tube``.

1) Create initial condition file
---------------------------------

A python script for generating the initial condition file (``create.py`` or ``create.ipynb``) is included in the directory. Detailed explanations will be given in the session. To open the Jupyter notebook file, use the following line,

.. code-block:: console

   $ jupyter notebook --no-browser --port <PORT>
   
Note that you should use the same <PORT> number that you used to log onto the compute node.
Then you will see the following messages:

.. code-block:: console

   $ [I 12:33:51.509 NotebookApp] JupyterLab extension loaded from ...
   $ [I 12:33:51.509 NotebookApp] ...
   $ To access the notebook, open this file in a browser:
   $    file://...
   $ Or copy and paste one of these URLs:
   $    http://localhost:<PORT>/?token=....
   $...
   
you can copy and paste the entire URL starting with http://localhost:<PORT>/?token=... to your favorite browser, which will browse and open files on your browser.


2) Create parameter file
-------------------------

A sample parameter file (``param.txt``) is included in the directory. Detailed explanations will be given in the session.

3) Create configuration file
-----------------------------

A configuration file (``Config.sh``) is included in the directory. Detailed explanations will be given in the session.

Compilation
======================================================
Let's do the part that first-time users would spend a long time on. As before, we will go through this step by step.

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
   $ module load anaconda3
   
2) Set SYSTYPE
------------------

To successfully compile almost every hydrodynamics code, it is very important to set the paths correctly to the dependences (e.g., those modules we just loaded) inside the code. As mentioned above, because the paths to the modules are different for dffierent machines, you have to set the paths for each machine you are using. Every code has a different file in which you need to set the paths. The file for ``AREPO`` is ``makefiles/systypes.make``. Fortunately, the system setups for the mpa cluster, raven, cobra, and freya were already set! All you need to do is to make sure that you tell the code correctly which system you are on. You can set the system type by,

.. code-block:: console

   $ export SYSTYPE=pascal

One convenient way is to add the line to your bash file (``~/.bashrc``) and do ``source ~/.bashrc`` instead of typing the line above.


3) Compile
---------------

We need a test case for which compile the code. To compile, you first go to the ``AREPO`` directory,

.. code-block:: console

   $ cd <MPA_path_to_your_directory>/
   
We will compile the code with the configuration file for the shock tube test with the following command,

.. code-block:: console

   $ make CONFIG=./run/Shock_tube/Config.sh BUILD_DIR=./run/Shock_tube/build EXEC=./run/Shock_tube/Arepo
   
If you increase the compilation speed by using multiple cores, you can add ``-j5`` (if you use 5 cpus) at the end of the line. If you do not see any errors and the compilation ends with the following lines,

.. code-block:: console

   $ ...... -L/opt/hdf5-1.8.18/lib -lhdf5 -Xlinker -R -Xlinker /opt/hdf5-1.8.18/lib -lmpi -lgsl -lgsl -lgslcblas   -lgmp               -o run/Shock_tube/Arepo
   $ Checking ./run/Shock_tube/build/Template-Config.sh.check and ./run/Shock_tube/build/defines_extra.check for duplicate options

you should see an executable ``Arepo``. Now you are ready to run!

A few tips
======================================================

These are few useful tips.

1. The AREPO domain with box size `L` starts from 0 to `L`, not `-L/2` to `L/2`. So you need to re-adjust the domain origin to make sure that (0, 0, 0) is at the bottom-left corner of the domain.

2. To comment out in the parameter file, use ``%``. However, use ``#`` to comment out in the configuration file.
