.. _Session3:

************************************************************************************
Session 3. Preparation - download and installation
************************************************************************************

Overview
================================================================
In this session, we will prepare for practice sessions. The codes that you will need are ``AREPO`` and ``Arepo-snap-util``.
``Arepo-snap-util`` is an analysis package designed and developed for ``AREPO`` simulations, which you will need to read output data and make plots from the data. Some of the steps enumerated here would be different depending on which machines you are on. Sections containing something only specific for the MPA cluster (except for directory paths) will be indicated with [*MPA]. Also the path to your directory on the MPA cluster will be indicated as ``<MPA_path_to_your_directory>``.

Download
=========

The codes are stored in ``/afs/mpa/temp/tryu/AREPO_tutorial/``. Once you log onto the mpa cluster, please go to the directory and copy both to your directory (you should have access to the directory by now. If not, please let me know):

.. code-block:: console

   $ cd <MPA_path_to_taeho's_directory>/AREPO_tutorial/
   $ cp -r * <MPA_path_to_your_directory>/
   

Installation
=============
To run ``AREPO``, you would need to install several programs (e.g., hdf5, mpi, and so on). However, all those required programs are installed on the MPA cluster. All you need to do is load proper environmental modules required for compiling and running ``AREPO`` simulations. However, you need to install ``Arepo-snap-util`` to use the built-in routines in the analysis package. Once you install it, you can call any functions of the code in your python scripts by adding a line ``from loadmodules import *`` to the header of your python scripts. Let's install ``Arepo-snap-util`` by following the follow steps.

1. Load modules
---------------
  
  Let's load a python module,

.. code-block:: console

   $ module load anaconda3 gsl

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

   $ cd <MPA_path_to_your_directory>/Arepo-snap-util

and add the following lines [*MPA],

.. code-block:: python

   incl_dirs = ['...']
   libs_dirs = ['...']

below ``#ADD PATH HERE`` in ``setup.py`` using your favorite editor (e.g., emacs). If you want to run ``AREPO`` on ``raven``, ``cobra`` or ``freya`` and analyze data there using this analysis package, please follow the same steps: the only difference would be that the path to ``gsl`` on a different machine is different (* cobra needs extra steps. If you want to run on cobra, please let me know).

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

you successfuly installed the package.

