UBEM and Thermal Coupling
=========================

Configuration file: ``Inp/CityScaLES.ubem``.

``Inp/CityScaLES.ubem`` selects the Urban Building Energy Model (UBEM)
coupling mode and specifies the files used to exchange data with
CityBEM or CityBES.


Coupling Mode
-------------

The parameter ``ubem_type`` selects the coupling mode and determines
whether the temperature equation is enabled.

.. list-table::
   :header-rows: 1
   :widths: 18 47 35

   * - ``ubem_type``
     - Coupling mode
     - Temperature equation
   * - ``0``
     - No UBEM coupling (supplied case)
     - Disabled (``thermal = 0``)
   * - ``1``
     - CityBEM coupling
     - Enabled (``thermal = 1``)
   * - ``2``
     - CityBES coupling
     - Enabled (``thermal = 1``)

In CityScaLES, thermal activation is tied to ``ubem_type``. The supplied
``CityScaLES.domain`` does not contain a separate ``thermal`` setting.


CityBEM Coupling
----------------

The following settings are used when ``ubem_type = 1``.

.. list-table::
   :header-rows: 1
   :widths: 42 58

   * - Parameter
     - Value in the supplied configuration
   * - ``citybem_in``
     - Output_CityBEM_Ts.txt
   * - ``citybem_out``
     - Input_CityBEM_Ts.txt

These parameters specify the filenames associated with the CityBEM
coupling interface.


CityBES Coupling
----------------

The following settings are used when ``ubem_type = 2``.

.. list-table::
   :header-rows: 1
   :widths: 42 58

   * - Parameter
     - Value in the supplied configuration
   * - ``citybes_static_json``
     - red_nodes.json
   * - ``cityscales_static_json``
     - blue_nodes.json
   * - ``cityscales_static_mapping``
     - merged_surface.txt
   * - ``citybes_dynamic_json_start``
     - 100
   * - ``citybes_dynamic_json_stride``
     - 100
   * - ``citybes_hdf5``
     - CityBES.h5

These parameters identify the static exchange files, surface mapping,
dynamic exchange settings, and HDF5 file used by the CityBES interface.


Configuring a Coupled Simulation
--------------------------------

To configure a CityBEM- or CityBES-coupled simulation:

1. Set ``ubem_type`` to the required coupling mode in
   ``Inp/CityScaLES.ubem``.

2. Provide the input and exchange files required by the selected
   coupling interface.

3. Verify that surface and building identifiers are consistent between
   the coupled models.

4. Confirm that temperature units are consistent.

5. Check the exchange sequence against the CityScaLES coupling
   implementation before running the coupled simulation.

