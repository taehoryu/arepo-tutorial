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

To use ``AREPO``, you don't need to install anything. What you need is proper environmental modules required for compiling and runnign ``AREPO`` simulations. However, you need to install ``Arepo-snap-util`` to use the built-in routines in the code. Once you install it, you can call any functions of the code in your python scripts by adding a line ``from loadmodules import *`` to the header of your python scripts. 
