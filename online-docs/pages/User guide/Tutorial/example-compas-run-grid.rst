Running COMPAS using a grid file
================================

In population synthesis, the initial stellar population is usually generated by drawing the primary mass, secondary mass, semi-major axis, 
and eccentricity from their respective distributions specified in the program options. However, we illustrate COMPAS's ability to specify 
a grid of initial values for single and binary star evolution using COMPAS's grid functionality.

An example grid file, ``Grid_demo.txt``, is included in the ``detailed_evolution`` directory. Open it with a text editor to view it::

    # Demo BSE Grid file

    --initial-mass-1 35.4 --initial-mass-2 29.3 --metallicity 0.001  --eccentricity 0.000000e+00 --semi-major-axis 1.02

It should be clear that this grid file specifies a binary of zero-age main sequence stars with primary mass 
35.4\ :math:`\small M_\odot`, secondary mass 29.3\ :math:`\small M_\odot`, metallicity 0.001, zero eccentricity, and semi-major axis of 
1.02AU. See :doc:`../grid-files` for detailed information regarding COMPAS's grid functionality for both single and binary stars.

We will execute COMPAS via the ``runSubmit.py`` script, but first we need to edit the companion ``compasConfigDefault.yaml`` script to instruct COMPAS to read the grid file
(via the ``grid`` program option).

Open ``$COMPAS_ROOT_DIR/preProcessing/compasConfigDefault.yaml`` with a text editor, and specify the grid filename::

    grid_filename = 'Grid_demo.txt'
    
Note the quotes around the filename. 

If the filename specified is not fully-qualified, and the shell environment variable ``COMPAS_INPUT_DIR_PATH`` exists and is not empty,
the value of ``COMPAS_INPUT_DIR_PATH`` will be prepended to the specified grid filename. 


To print the detailed evolution of binary properties over time, we need to turn on detailed output, by specifying::

    detailed_output = True

in ``compasConfigDefault.yaml``.

COMPAS can produce logfiles of different types: ``HDF5``, ``CSV``, ``TSV``, and ``TXT``, which can be chosen by editing the line::

    logfile_type = 'HDF5'

in ``compasConfigDefault.yaml``. The default type is ``HDF5`` - we'll leave the default.

NOTE: we are currently updating our documentation and will include a ``compasConfigDefault.yaml`` for the demo asap.

..
    For this tutorial, this has all been done for you in the file ``pythonSubmitDemo.py`` found in the ``examples/methods_paper_plots/detailed_evolution/`` directory.

..
    Now let's run COMPAS!

..
    ::

        $ python3 pythonSubmitDemo.py

        COMPAS v02.18.06
        Compact Object Mergers: Population Astrophysics and Statistics
        by Team COMPAS (http://compas.science/index.html)
        A binary star simulator

        Start generating binaries at Thu Feb 25 14:42:05 2021

        Evolution of current binary stopped: Double compact object
        0: Evolution stopped: (Main_Sequence_>_0.7 -> Black_Hole) + (Main_Sequence_>_0.7 -> Black_Hole)

        Generated 1 of 1 binaries requested

        Simulation completed

        End generating binaries at Thu Feb 25 14:42:05 2021

        Clock time = 0.108338 CPU seconds
        Wall time  = 00:00:00 (hh:mm:ss)

..
    Congratulations! You've just made a binary black hole. And it didn't even take a second.
