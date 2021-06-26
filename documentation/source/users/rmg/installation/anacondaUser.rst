.. _anacondaUser:

****************************************************************************
Binary Installation Using Anaconda for Unix-Based Systems: Linux and Mac OSX
****************************************************************************


#. Download and install the `Anaconda Python Platform <https://www.anaconda.com/download/>`_ for Python 3.7.

   The download will be a .sh file with a name like ``Anaconda3-2019.07-Linux-x86_64.sh``. Open a terminal in the same
   directory as this file, and type the following to install Anaconda (replace the name of your .sh file below). ::

    bash Anaconda3-2019.07-Linux-x86_64.sh

   **When prompted to append Anaconda to your PATH, select or type Yes**.  Install the Anaconda folder inside your home directory (typically ``/home/YourUsername/`` in Linux and ``/Users/YourUsername`` in Mac). When prompted, you do not need to install Microsoft VSCode (but feel free to if you are looking for a lightweight IDE).

#. Install both RMG and the RMG-database binaries through the terminal.   Dependencies will be installed automatically. It is safest to make a new conda environment for RMG and its dependencies. Type the following command into the terminal to create the new environment named 'rmg_env' containing the latest stable version of the RMG program and its database. ::

    conda create -c defaults -c rmg -c rdkit -c cantera -c pytorch -c conda-forge --name rmg_env rmg rmgdatabase
    
   Whenever you wish to use it you must first activate the environment::
    
    source activate rmg_env

#. Install and Link Julia dependencies ::

    python -c "import pyrms; pyrms.install()"
    ln -sfn $(which python-jl) $(which python)
       
    Note that this links your python to python-jl enabling calls to Julia through pyjulia. Occasionally programs will 
    interact with python-jl differently than the default python. If this occurs for you we recommend doing that operation
    in a different conda environment. However, if convenient you can undo this linking by replacing python-jl with 
    python3 in the second command above. Just make sure to rerun the linking command once you are done. 
       
#. Optional: If you wish to use the :ref:`QMTP interface <qm>` with `MOPAC <http://openmopac.net/>`_ to run quantum mechanical calculations for improved thermochemistry estimates of cyclic species, please obtain a legal license through the `MOPAC License Request Form <http://openmopac.net/form.php>`_.  Once you have it, type the following into your terminal ::
    
    mopac password_string_here

#. You may now run an RMG test job. Save the `Minimal Example Input File <https://raw.githubusercontent.com/ReactionMechanismGenerator/RMG-Py/master/examples/rmg/minimal/input.py>`_
   to a local directory.  Use the terminal to run your RMG job inside that folder using the following command ::

    rmg.py input.py

You may now use RMG-Py, Arkane, as well as any of the :ref:`Standalone Modules <modules>` included in the RMG-Py package.


Updating your binary installation of RMG in Linux or Mac OSX
============================================================

If you had previously installed a binary version of the RMG package, you may
check and update your installation to the latest stable version available on Anaconda by typing the following command on the terminal ::

    source activate rmg_env
    conda update rmg rmgdatabase -c rmg 
