.. _Session6:

************************************************************************************
Session 6. Practice 1 - relaxation of main-sequence star
************************************************************************************

1. Creating 3D star
==================================
A python script to make a single main-sequence star can be found in ``run/Star_relaxation/Creating_IC``. In the directory, you can find the following files,

.. code-block:: console

   $ MESAmodel  helm_table.dat  ic_MS.py  module.py    param_config_sample  snapshot_single.py  species55.txt

``MESAmodel`` contains MESA models that will be mapped into a 3D domain. You can see two stellar models, one for a 0.3Msol star (``MESA_0.3Msol_Z0.020_H0.69.data``) and one for a 1Msol star (``MESA_1Msol_Z0.02_H0.5.data``). 
