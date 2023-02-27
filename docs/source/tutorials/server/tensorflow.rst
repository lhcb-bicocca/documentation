Running Tensorflow
##################

For running Tensorflow with the GPU it is recommended to follow the subsequent instructions.

Install Tensorflow
******************

The simplest is to install Tensorflow via ``MiniConda`` following the instructions at `this page <https://www.tensorflow.org/install/pip?hl=it#step-by-step_instructions>`_

First install MiniConda

.. code-block:: bash

    curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh

Then create a *Conda* environment with

.. code-block:: bash

    conda create --name tf python=3.9

Activate the environment and install CUDA and cuDNN with conda

.. code-block:: bash

    conda activate tf
    conda install -c conda-forge cudatoolkit=11.2.2 cudnn=8.1.0

Correctly setup the environment anytime you activate the *tf* environment

.. code-block:: bash

    mkdir -p $CONDA_PREFIX/etc/conda/activate.d
    echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/' > $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh

Finally install tensorflow

.. code-block:: bash

    pip install --upgrade pip
    pip install tensorflow==2.11.*

Testing the Installation
========================

For testing the installation run 

.. code-block:: bash

    python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

This should output something like

.. code-block:: bash

    $ python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
    2023-02-27 11:56:37.102410: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 AVX512F AVX512_VNNI FMA
    To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
    2023-02-27 11:56:37.308108: I tensorflow/core/util/port.cc:104] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
    2023-02-27 11:56:38.204524: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer.so.7'; dlerror: libnvinfer.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: :/home/maurizio/miniconda3/envs/tf/lib/
    2023-02-27 11:56:38.204638: W tensorflow/compiler/xla/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libnvinfer_plugin.so.7'; dlerror: libnvinfer_plugin.so.7: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: :/home/maurizio/miniconda3/envs/tf/lib/
    2023-02-27 11:56:38.204656: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Cannot dlopen some TensorRT libraries. If you would like to use Nvidia GPU with TensorRT, please make sure the missing libraries mentioned above are installed properly.
    2023-02-27 11:56:39.040308: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 AVX512F AVX512_VNNI FMA
    To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
    2023-02-27 11:56:39.920818: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1613] Created device /job:localhost/replica:0/task:0/device:GPU:0 with 78950 MB memory:  -> device: 0, name: NVIDIA A100 80GB PCIe, pci bus id: 0000:b1:00.0, compute capability: 8.0
    tf.Tensor(1628.1882, shape=(), dtype=float32)

The warnings on the ``libnvinfer`` library are due to tensorrt package missing.
You can install it by calling 

.. code-block:: bash

    pip install nvidia-pyindex
    pip install nvidia-tensorrt

Even without it Tensorflow will still work.

If the libraries are still not found and the warning message upsets you, you could try to symlink them (at your own risk!)

.. code-block:: bash
    
    ln -s $HOME/miniconda3/envs/tf/lib/python3.9/site-packages/tensorrt/libnvinfer.so.8 $HOME/miniconda3/envs/tf/lib/libnvinfer.so.7
    ln -s $HOME/miniconda3/envs/tf/lib/python3.9/site-packages/tensorrt/libnvinfer_plugin.so.8 $HOME/miniconda3/envs/tf/lib/libnvinfer_plugin.so.7
    ln -s $HOME/miniconda3/envs/tf/lib/python3.9/site-packages/tensorrt/libnvonnxparser.so.8 $HOME/miniconda3/envs/tf/lib/libnvonnxparser.so.7
    ln -s $HOME/miniconda3/envs/tf/lib/python3.9/site-packages/tensorrt/libnvparsers.so.8 $HOME/miniconda3/envs/tf/lib/libnvparsers.so.7

Similarly you can test that Tensorflow sees the GPU

.. code-block:: bash

    python3 -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"

that, apart the previous warnings, should return

.. code-block:: bash

    [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]

Running TensorFlow
******************
