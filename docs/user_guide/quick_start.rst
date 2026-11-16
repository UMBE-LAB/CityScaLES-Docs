Getting Started
===============

Case Directory Structure
------------------------

A typical CityScaLES case uses the following files and directories.

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Path relative to case root
     - Purpose

   * - ``CityScaLES_prepro``
     - Preprocessing executable.

   * - ``CityScaLES_solver``
     - Flow-solver executable.

   * - ``Inp/``
     - Directory for input data.

   * - ``Tag/``
     - Directory for preprocessing data.

   * - ``Out/``
     - Directory for simulation results.

   * - ``CityScaLES.domain``
     - Main domain, numerical, boundary-condition, and output controls.

   * - ``Inp/CityScaLES.cfg``
     - MPI process grid, CPU threads, and CUDA block sizes.

   * - ``Inp/CityScaLES.cfd``
     - Cartesian domain lengths, cell counts, and cell-width lists.

   * - ``Inp/building.stl``
     - Triangulated building geometry.

   * - ``Inp/CityScaLES.met``
     - Meteorological source selector and source filename.

   * - ``Inp/CityScaLES.weather``
     - Meteorological records used to prescribe wind and environmental conditions.

   * - ``Inp/CityScaLES.ubem``
     - UBEM selection and coupling filenames.

   * - ``Inp/CityScaLES.probe``
     - Probe IDs, coordinates, and sampling window.

   * - ``Inp/CityScaLES.state``
     - Startup mode, restart-file selection, and checkpoint settings.


Before the First Run
--------------------

1. Prepare a working directory for the simulation.

   Place ``CityScaLES.domain`` in this directory.
   Place the required input files in the ``Inp/`` subdirectory.

   Create the ``Tag/`` and ``Out/`` subdirectories for preprocessing
   data and simulation results, respectively.

2. Place ``CityScaLES_prepro`` and ``CityScaLES_solver`` in the working
   directory, or create symbolic links to them.

   Ensure that both executables are compatible with the target system
   and have execute permissions.

3. Configure the simulation inputs and computational resources.

   Specify the domain, mesh, boundary conditions, physical models,
   meteorological inputs, and output settings in the corresponding
   input files.

   Set the MPI process counts and CPU/GPU thread settings in
   ``Inp/CityScaLES.cfg``.

4. Configure the startup mode in ``Inp/CityScaLES.state``.

5. From the working directory, run ``CityScaLES_prepro`` to prepare the
   simulation data.

   Check that preprocessing completes successfully before launching
   ``CityScaLES_solver``.

6. Launch ``CityScaLES_solver``.

7. Monitor the simulation log and inspect the probe and flow-field
   outputs during and after the simulation.


