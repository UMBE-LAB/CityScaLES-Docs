Restart and Checkpoint
======================

Configuration file: ``Inp/CityScaLES.state``.

``Inp/CityScaLES.state`` controls the startup mode, the input state-file
name, and the checkpoint-writing interval for CityScaLES.


Startup Mode
------------

The parameter ``start_mode`` selects how the flow field is initialized.

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - ``start_mode``
     - Description
   * - ``0``
     - Start from a fresh flow field.
   * - ``1``
     - Restart from a previously saved state file.
   * - ``2``
     - Initialize from an external initial file.

For a new simulation, set ``start_mode = 0``. To resume from a saved
state, set ``start_mode = 1``.


State File
----------

The parameter ``state_file`` specifies the file to be read when
starting from a saved or external state, depending on ``start_mode``.

For example:

.. code-block:: text

   start_mode = 1
   state_file = CityScaLES_rst.h5

This requests a restart from ``CityScaLES_rst.h5``.  The restart data file 
must be placed in the **case root directory**,


Checkpoint Writing
------------------

The parameter ``checkpoint_interval`` controls checkpoint writing.
The supplied configuration contains:

.. code-block:: text

   checkpoint_interval = 2000

The unit of this interval should be confirmed from the solver
implementation; it is not specified in the setting file itself.


Two Checkpoint Files
--------------------

CityScaLES outputs **at most two restart files**, which store solution
states saved at **two different iterations**:

* ``CityScaLES_rst.1.h5``
* ``CityScaLES_rst.2.h5``

Both checkpoint files are written in the **case root directory**,
alongside ``CityScaLES.domain``. They are not stored in an internal
subdirectory.

Either file can be selected as the starting point for a restart. The
suffixes ``.1`` and ``.2`` are file identifiers; they should not be
used on their own to determine which file represents the later
iteration. Select the file corresponding to the intended saved state.

To restart using the configured file name ``CityScaLES_rst.h5``, copy or
rename the selected checkpoint to that name. **Copying is recommended**
because it preserves the original checkpoint file.

For example, to use ``CityScaLES_rst.1.h5``, run the following command
in the directory containing the checkpoint files:

.. code-block:: bash

   cp CityScaLES_rst.1.h5 CityScaLES_rst.h5

Alternatively, to use ``CityScaLES_rst.2.h5``:

.. code-block:: bash

   cp CityScaLES_rst.2.h5 CityScaLES_rst.h5

.. important::

   The copy commands overwrite an existing ``CityScaLES_rst.h5``. Preserve
   any state file you may need before executing them. The selected restart file must be placed in the case root
   directory, alongside ``CityScaLES.domain``.


Restart Procedure
-----------------

To continue a simulation from a saved iteration:

1. In the case root directory (the same directory as
   ``CityScaLES.domain``), locate the checkpoint files, if both have
   been written: ``CityScaLES_rst.1.h5`` and ``CityScaLES_rst.2.h5``.

2. Choose the checkpoint corresponding to the iteration from which
   the simulation should resume.

3. Copy the selected checkpoint to the name specified by ``state_file``.
   For example:

   .. code-block:: bash

      cp CityScaLES_rst.1.h5 CityScaLES_rst.h5

4. In ``Inp/CityScaLES.state``, set:

   .. code-block:: text

      start_mode = 1
      state_file = CityScaLES_rst.h5

5. Set ``checkpoint_interval`` as needed for subsequent checkpoint
   writing.

6. Keep the case configuration compatible with the saved state, then
   launch ``CityScaLES_solver``. Check the solver output to confirm that
   the requested state was loaded.

.. note::

   The checkpoint and restart data files reside in the case root,
   while the startup settings are stored in ``Inp/CityScaLES.state``.
   Whether changing the MPI/GPU decomposition is supported for a
   restart has not been established here.

