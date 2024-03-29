Bicocca INFN Sever
##################
We have a server running in the cluster of the MIB INFN section.
The server runs on a CentOS7 operating system and features

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
- afs
- cuda12.0
- gcc11.2.1
- ROOT v6.26/10
- docker

For any further request, please contact **brownie-admins@lists.mib.infn.it**.
 
Please note that to access your *afs* and *eos* area, you should first create your afs token by ``kinit`` and connect it to the *eos* service.
We wrote a script to allow this in one shot

.. code-block:: console

  $ initialise_afs_and_eos.sh <cern_user_name>

By default the system is built on ``gcc4.8.5``. If you want to compile your programs in ``gcc11``, simply run

.. code-block:: console
 
  $ scl enable devtoolset-11 bash

The CUDA libraries are not automatically available at login, to load them (and enable gcc11)

.. code-block:: console
  
  $ load_cuda_environment.sh

To load ROOT into the environment

.. code-block:: console

  $ scl enable devtoolset-11 bash
  $ source /usr/local/root_src/root_v62610_gcc11_py3/bin/thisroot.sh

Please note that there could be some problems with ROOT `RConfig.hxx` in this install area that would make compilations of other packages depending on ROOT fail (e.g. GooFit). Therefore, unless a standalone ROOT compilation is needed, it is best to load the `LCG <https://lcginfo.cern.ch>`_ environment from cvmfs

.. code-block:: console

  $ source /cvmfs/sft.cern.ch/lcg/views/setupViews.sh LCG_102b x86_64-centos7-gcc11-opt

Storage
*******
Storage is divided in three areas

- ``/`` 3.7TB of SSD. This is where the **/home** folders are located.
- ``/data01`` 17.5TB of HDD. Use it for long term storage and backup.
- ``/data02`` 17.5TB of HDD. Use it for long term storage and backup.

The SSD disk is much faster than HDD, plese take this in consideration when running your programs.
A **scratch** area is located at ``/scratch/gr1/lhcb``. Please use it sensibly. Checks will be performed routinely to delete file not accessed for long.
