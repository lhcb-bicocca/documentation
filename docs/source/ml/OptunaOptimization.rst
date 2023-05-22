
Optuna Hyperparameter Optimization
##################################

Hyperparameter Optimization with Optuna on cluster GPU Bicocca.
Optuna is an automatic hyperparameter optimization software framework, particularly designed for machine learning.
Documentation: https://optuna.readthedocs.io/.

Optuna can be installed with pip. Python 3.7 or newer is supported.

.. code-block:: console

 pip install optuna

Optuna Dashboard is a real-time web dashboard for Optuna. You can check the optimization history, hyperparameter importances, etc. in graphs and tables.

.. code-block:: console
 pip install optuna-dashboard


A python DEMO code can be found here: https://github.com/Mmozzanica5/documentation/blob/optuna/docs/source/ml/readme.md

The example dataset is taken from: <https://scikit-learn.org/stable/datasets/toy_dataset.html>

!! The GPU code is designed to allocate different GPUs to different scripts running simultaneously but the Cluster GPU Bicocca has a single GPU available. This means one can only run one GPU-accelerated script at a time. Since there is only one GPU resource available, it can only be allocated to one script or process at any given moment. If you have multiple scripts that require GPU acceleration and need to run them simultaneously, you will have to wait for the currently running script to finish before starting the next one.






