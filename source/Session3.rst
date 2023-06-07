.. _Session3:

************************************************************************************
Session 3. Preparation - download and installation
************************************************************************************

Overview
================================================================
The codes that you will need are ``AREPO`` and ``Arepo-snap-util``.
There are four steps until you run hydrodynamics simulations using AREPO and analyze data from the simulations.

1) Creating initial condition files - ``Arepo-snap-util``
2) Compiling - ``AREPO``
3) Running  -  ``AREPO``
4) Analyzing  - ``Arepo-snap-util``

You can see which code will be used at each step.
``Arepo-snap-util`` is an analysis package designed and developed for ``AREPO`` simulations, which you will need to creat initial condition files, read output data and make plots from the data. This code has been developed and managed by Ruediger Pakmor (rpakmor@MPA-Garching.MPG.DE). In this session, we will first download both codes and install ``Arepo-snap-util`` (you do not need to install ``AREPO``, but probably its dependent programs)

Note that some of the steps enumerated here would be different depending on which machines you are on. Sections or explanations containing something only specific to the MPA cluster (except for directory paths) will be indicated with [*MPA]. Also, the path to your directory on the MPA cluster will be shown as ``<MPA_path_to_your_directory>``.

   
Access to cluster
=================
We will create the initial setup files and make plots using Jupyter notebook. So instead of doing ``ssh <yourid>@<address>``, we access to the cluster using the following line,

.. code-block:: console

   $ ssh -L <PORT>:localhost:<PORT> <yourid>@<address>
   
where you can pick a random number for <PORT>, e.g., <PORT> = 8080 or 10331. Then we will log onto the designated compute note named ``<nodename>`` (which I will tell you during the tutorial) using the following line,

.. code-block:: console

   $ ssh -L <PORT>:localhost:<PORT> <nodename>

All the tutorial seesions will be done on the designated node. Or if you follow this tutorial on your own, you can be on any of the computes nodes.


Download
=========

You can download a zip file containing the codes using the link to Datashare. Then you need to transfer the file to your own directory on the MPA cluster and unzip it. Then you can see the following directories

.. code-block:: console

   $ AREPO Arepo-snap-util
   

Installation
=============
To run ``AREPO``, you would need to install several dependent programs (e.g., hdf5, mpi, gsl, and fftw). However, all those programs are already installed on the MPA cluster. So you don't need to install anything and all you need to do is load proper environmental modules required for compiling and running ``AREPO`` simulations.

However, you need to install ``Arepo-snap-util`` to use its built-in routines. Once you install it, you can call any functions of the code in your python scripts by adding a line ``from loadmodules import *`` to the header of your python script. Let's install ``Arepo-snap-util``.

1. Load modules
---------------
  
Let's load the python and gsl modules,

.. code-block:: console

   $ module load python3 gsl

[*MPA]

2. Set the path to ``gsl``
---------------------------

We need to set the path to the ``gsl`` module in ``setup.py``. Let's first find out the path to ``gsl`` by using the following line,

.. code-block:: console

   $ module show gsl

which will give the following information,

.. code-block:: console

   $ -------------------------------------------------------------------
   $ ..../gsl/2.4:
   $ module-whatis    ....
   $ prepend-path    PATH    ...
   $ prepend-path    LD_LIBRARY_PATH    ....
   $ -------------------------------------------------------------------

The path to ``gsl`` is next to ``PATH``. Now go to the ``Arepo-snap-util`` directory,

.. code-block:: console

   $ cd <MPA_path_to_your_directory>/AREPO_tutorial/Arepo-snap-util

and add the following lines [*MPA],

.. code-block:: python

   incl_dirs = ['.../include']
   libs_dirs = ['.../lib']

below ``#ADD PATH HERE`` in ``setup.py`` using your favorite editor (e.g., emacs). Here, '...' should be replaced with the path to gsl. If you want to analyze data on ``raven``, ``cobra`` or ``freya`` using the same analysis package, please follow the same steps above: the only difference would be that you will need to use the proper path to ``gsl`` on the machine you are on (* cobra needs extra steps. If you want to run on cobra, please let me know).

3. Install the package
-----------------------

Finally, let's install with the following command,

.. code-block:: console

   $ python3 setup.py install --user

If you do not see any errors and the installation ends with,

.. code-block:: console

   $ ...
   $ running install_clib
   $ customize UnixCCompiler
   
or

.. code-block:: console

   $ ########### EXT COMPILER OPTIMIZATION ###########
   $ ...
   $ CPU baseline  :
   $ ...
   $ CPU dispatch  :
   $ ...
   $ INFO: ...
   
that means you have successfuly installed the package.

