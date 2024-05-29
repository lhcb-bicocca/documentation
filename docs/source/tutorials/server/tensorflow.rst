Running Tensorflow
##################

For running Tensorflow with the GPU it is recommended to follow the subsequent instructions.

Install Tensorflow
******************

The simplest is to install Tensorflow in a virtual environment with ``pip`` following the instructions at `this page <https://www.tensorflow.org/install/pip?hl=it#step-by-step_instructions>`_

First create a virtual environment in a directory of choice

.. code-block:: bash

    python3 -m venv environments/tf

Then activate the environment and install tensorflow

.. code-block:: bash

    source environments/tf/bin/activate
    pip install --upgrade pip
    pip install tensorflow[and-cuda]

Correctly setup the environment anytime you activate the *tf* environment.
Add the following lines at the bottom of `environments/tf/bin/activate`

.. code-block:: bash

    _OLD_CUDNN_PATH="$CUDNN_PATH"
    CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))
    export CUDNN_PATH

    _OLD_LD_LIBRARY_PATH="$LD_LIBRARY_PATH"
    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CUDNN_PATH/lib
    export LD_LIBRARY_PATH

If you want these variables to be properly unset once the environment is closed also add these commands to the `deactivate` function in `environments/tf/bin/activate`

.. code-block:: bash

    if [ -n "${_OLD_CUDNN_PATH:-}" ] ; then
        CUDNN_PATH="${_OLD_CUDNN_PATH:-}"
        export CUDNN_PATH
        unset _OLD_CUDNN_PATH
    else
        unset CUDNN_PATH
    fi
    if [ -n "${_OLD_LD_LIBRARY_PATH:-}" ] ; then
        LD_LIBRARY_PATH="${_OLD_LD_LIBRARY_PATH:-}"
        export LD_LIBRARY_PATH
        unset _OLD_LD_LIBRARY_PATH
    else
        unset LD_LIBRARY_PATH
    fi

Testing the Installation
========================

For testing the installation run 

.. code-block:: bash

    python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

This should output something like

.. code-block:: bash

    $ python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
    2024-05-29 15:51:35.800278: I tensorflow/core/util/port.cc:113] oneDNN custom operations are on. You may see slightly different numerical results due to floating-   point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
    2024-05-29 15:51:35.843378: I tensorflow/core/platform/cpu_feature_guard.cc:210] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
    To enable the following instructions: AVX2 AVX512F AVX512_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
    2024-05-29 15:51:36.450537: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
    2024-05-29 15:51:37.114986: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1928] Created device /job:localhost/replica:0/task:0/device:GPU:0 with 79061 MB memory:  -> device: 0, name: NVIDIA A100 80GB PCIe, pci bus id: 0000:b1:00.0, compute capability: 8.0
    tf.Tensor(264.08917, shape=(), dtype=float32)


You may notice that there are warnings about tensorrt package missing.
.. You can install it by calling 
..
.... code-block:: bash
..
..    #pip install nvidia-pyindex #kept since 
..    pip install nvidia-tensorrt
..
Even without it Tensorflow will still work. 
Get in touch with the administrators to install it if needed.

Similarly you can test that Tensorflow sees the GPU

.. code-block:: bash

    python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"

that, apart the previous warnings, should return

.. code-block:: bash

    [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]

Running TensorFlow
******************

Simply activate the environment

.. code-block:: bash

    source environments/tf/bin/activate

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
