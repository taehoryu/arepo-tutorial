.. _Session3:

************************************************************************************
Session 3. Preparation - download and installation
************************************************************************************

Overview
================================================================
The codes that you will need are ``AREPO`` and ``Arepo-snap-util``.
There are four big steps in running hydrodynamics simulations using AREPO.

1) Creating initial condition files - `Arepo-snap-util``
2) Compiling - ``AREPO``
3) Running  - `Arepo-snap-util``
4) Analyzing  - ``AREPO``


``Arepo-snap-util`` is an analysis package designed and developed for ``AREPO`` simulations, which you will need to read output data and make plots from the data. Some of the steps enumerated here would be different depending on which machines you are on. Sections containing something only specific for the MPA cluster (except for directory paths) will be indicated with [*MPA]. Also the path to your directory on the MPA cluster will be indicated as ``<MPA_path_to_your_directory>``.

Download
=========

You can download a zipped file containing the codes using the link to Datashare. Then you need to transfer the file to your directory on the MPA cluster and unzip it. Then you can see the follow directories

.. code-block:: console

   $ AREPO Arepo-snap-util
   
Installation
=============
To run ``AREPO``, you would need to install several dependent programs (e.g., hdf5, mpi, gsl, and fftw). However, all those programs are already installed on the MPA cluster. So you don't need to install anything and all you need to do is load proper environmental modules required for compiling and running ``AREPO`` simulations.

However, you need to install ``Arepo-snap-util`` to use its built-in routines. Once you install it, you can call any functions of the code in your python scripts by adding a line ``from loadmodules import *`` to the header of your python script. Let's install ``Arepo-snap-util``.

1. Load modules
---------------
  
Because we will compile and run the test simulations on ``XX`` node, let's first access the node using,

.. code-block:: console

   $ ssh XX

Then, let's load the python and gsl modules,

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

