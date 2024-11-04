Bicocca INFN Sever
##################
We have a server running in the cluster of the MIB INFN section.
The server runs on a Alma9 operating system and features

- NVIDIA A100 80Gb GPU
- 2x26 core Intel Xeon 5320 2.2GHz CPU
- 256Gb RAM
- 3x1920Gb SSD SATAIII disks
- 4x18Tb SATAIII 7200rpm HDD disks

Requesting an account
*********************
The server is connected to the accounting system of the MIB INFN section.
First you need to have a valid computing account with MIB-INFN and then you can ask for access to the server by sending an email to **brownie-admins@lists.mib.infn.it**.
Once approved, you will be available to connect with the username and password of your MIB account.

You will also be added to the brownie users' mailing list (**brownie-users@lists.mib.infn.it**). 
Feel free to send messages to this list for discussing troubles or software requests.

Connection
==========

Connections are allowed only from within the local network. If you are connecting from outside, please remember to login to the gateway *cerbero* first.
There are two options to connect in one command. Either

.. code-block:: console

 $ ssh -J <user_name>@cerbero.mib.infn.it <user_name>@brownie
 
or add the following lines to your ``.ssh/config``:

.. code-block:: console

 Host brownie.mib.infn.it
   ProxyCommand ssh -W %h:%p <user_name>@cerbero.mib.infn.it

Note that the latest will allow you to use VisualStudio Code connection to the remote host to modify directly files on the server.

Services
********
Available services include:

- cvmfs
- eos
- docker

For any further request, please contact **brownie-admins@lists.mib.infn.it**.
 
Please note that to access your *eos* area, you should first create your afs token by ``kinit``:

.. code-block:: console

  $ kinit <cern_user_name>@CERN.CH

.. The CUDA libraries are not automatically available at login, to load them
..
.. .. code-block:: console
..  
..  $ load_cuda
..
To use ROOT the simplest is to load an environment from cvmfs

.. code-block:: console

  $ source /cvmfs/sft.cern.ch/lcg/views/setupViews.sh LCG_105b x86_64-el9-gcc13-opt

be reminded of loading libraries compiled for `x86_64-el9`. 
A complete list of libraries for each LCG version can be found at this `address <https://lcginfo.cern.ch>`_.

Storage
*******
Storage is divided in three areas

- ``/`` 3.7TB of SSD. This is where the **/home** folders are located.
- ``/data01`` 17.5TB of HDD. Use it for long term storage and backup.
- ``/data02`` 17.5TB of HDD. Use it for long term storage and backup.

The SSD disk is much faster than HDD, plese take this in consideration when running your programs.
A **scratch** area is located at ``/scratch/gr1/lhcb``. Please use it sensibly. Checks will be performed routinely to delete file not accessed for long.
