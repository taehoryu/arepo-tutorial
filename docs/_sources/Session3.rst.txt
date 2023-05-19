.. _Session3:

************************************************************************************
Session 3. Preparation - download, installation, and compilation
************************************************************************************

Overview
================================================================
In this session, we will prepare for the practice sessions. The codes that you will need are ``AREPO`` and ``Arepo-snap-util``.
``Arepo-snap-util`` are an analysis package designed and developed for ``AREPO`` simulations, which you will need to read output data and make plots from the data.

1) download

The codes are stored in ``/afs/mpa/temp/tryu/AREPO_tutorial/``. So once you log onto the mpa cluster, please go to the directory and copy both to your directory (you should have access to my directory by now. If not, please let me know):

.. code-block:: console

   $ cd /afs/mpa/temp/tryu/AREPO_tutorial/
   $ cp -r * /afs/mpa/temp/<path_to_your_directory>/
   

2) installation

To use ``AREPO``, you don't need to install anything. What you need is proper environmental modules required for compiling and runnign ``AREPO`` simulations. However, you need to install ``Arepo-snap-util`` to use the built-in routines in the code. Once you install it, you can call any functions of the code in your python scripts by adding a line ``from loadmodules import *`` to the header of your python scripts. To install ``Arepo-snap-util'', you follow several steps.

  - load modules.
  
  Let's load a python module,

.. code-block:: console

   $ module load anaconda3 gsl

  - set the path to ``gsl``
  
Then go to the ``Arepo-snap-util'' directory,

.. code-block:: console

   $ cd /afs/mpa/temp/<path_to_your_directory>/Arepo-snap-util

we need to set the path to ``gsl`` module in ``setup.py``. You can see the path to the module with the following line,

.. code-block:: console

   $ module show gsl

which will give the following information,

.. code-block:: console

   $ -------------------------------------------------------------------
   $ /usr/common/share/modulefiles/MPA/libs/gsl/2.4:
   $ module-whatis    Enables usage of gsl 2.4
   $ prepend-path    PATH    /opt/gsl-2.4/bin
   $ prepend-path    LD_LIBRARY_PATH    /opt/gsl-2.4/lib
   $ -------------------------------------------------------------------

The path to ``gsl`` is next to ``PATH``. Now add the following lines,


below ``#ADD PATH HERE`` in ``setup.py`` using your favorite editor (e.g., emacs). If you want to run AREPO on ``raven``, ``cobra`` or ``freya`` and want to analyze data there using this analysis package, please follow the same steps: the only difference would be that the path to ``gsl`` on a different machine is different (* cobra needs extra steps. If you want to run on cobra, please let me know).

  - install the package
  
Finally, let's install with the following command,

.. code-block:: console
    # python3 setup.py install --user
