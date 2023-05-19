.. _Session4:

************************************************************************************
Session 4. Making initial condition files and compile
************************************************************************************



1. Make initial condition files
======================================================

For each physics problem that you want to study using AREPO, you have to create an initial condition files which describes the initial state of the system that you are interested in. To compile the code, you need `Config.sh` file which contains necessary configurations. For example, 


2. Compilation
======================================================
Let's do the part that first-time users spent a long time on. As before, we will go through this step by step.

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
