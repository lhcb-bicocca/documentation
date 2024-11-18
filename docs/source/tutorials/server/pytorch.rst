Running PyTorch
###############

For running PyTorch with the GPU it is recommended to follow the subsequent instructions.

Install PyTorch
***************

The simplest is to install PyTorch in a virtual environment with ``pip`` following the instructions at `this page <https://pytorch.org/get-started/locally/>`_

First create a virtual environment in a directory of choice

.. code-block:: bash

    python3 -m venv environments/pytorch

Then activate the environment and install PyTorch

.. code-block:: bash

    source environments/pytorch/bin/activate
    pip install --upgrade pip
    pip install torch torchvision torchaudio


Testing the Installation
========================

For testing the installation run 

.. code-block:: bash

    python3 -c "import torch; print(torch.cuda.is_available())"

This should output `True`.

Running PyTorch
***************

Simply activate the environment

.. code-block:: bash

    source environments/pytorch/bin/activate

If you want to open a jupyter notebook, install it in case it was not installed 

.. code-block:: bash

    pip install jupyter

And open a jupyter session

.. code-block:: bash

    jupyter notebook

This will open a browser page with jupyter.
In case you are working outside the mib.infn.it domain, you should ssh tunnel to the server.
In your laptop's shell

.. code-block:: bash

    ssh -NL 1234:localhost:1234 <user_name>@brownie.mib.infn.it

and keep the terminal window open.
Then on the server

.. code-block:: bash

    jupyter notebook --no-browser --port 1234

now you can open the ``http://localhost:1234/?token=<token>`` link in your laptop's browser and use jupyter as if you were using brownie's browser.
