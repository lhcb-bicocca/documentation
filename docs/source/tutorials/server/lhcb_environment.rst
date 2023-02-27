Running the LHCb Environment
############################

The LHCb environment can be loaded by calling

.. code-block:: bash

    $ source /cvmfs/lhcb.cern.ch/lib/LbEnv

It is also possible to access directly AFS and EOS with your credentials by calling the script

.. code-block:: bash

    $ initialise_afs_and_eos.sh <cern_user_name>

GRID Proxy
**********

To load your GRID proxy to the server you should create a ``.globus`` directory in your home and copy the Grid certificate from lxplus

.. code-block:: bash

    $ mkdir $HOME/.globus
    $ cp <your_afs_cern_home>/.globus/{usercert,userkey}.pem $HOME/.globus/.

To test that the GRID certificate is loaded correctly, prompt 

.. code-block:: bash

    $ lhcb-proxy-init

Ganga
*****

It is possible to run Ganga on the server. Simply

.. code-block:: bash

    $ source /cvmfs/lhcb.cern.ch/lib/LbEnv
    $ ganga

After the first call to ``ganga``, the program will create the file ``.gangarc``. 
If you want to change the ``gangadir`` directory from the default ``/home/<user_name>/gangadir``, specify it there.
It is advisable to save the gangadir to the SSD disk since it is faster to access.