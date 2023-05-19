
Optuna Hyperparameter Optimization
##################################

Hyperparameter Optimization with Optuna on cluster GPU Bicocca

The example dataset is taken from: <https://scikit-learn.org/stable/datasets/toy_dataset.html>


.. code-block:: python
 import time
 import datetime
 import tensorflow as tf
 import os,sys
 #import pygraphviz as pgv
 import numpy as np
 import networkx as nx
 import matplotlib.pyplot as plt
 import subprocess, re
  import xgboost as xgb
  import optuna
  from optuna.samplers import TPESampler
  import csv
  from csv import DictWriter
  from csv import writer
  import sklearn
  #example dataset from sklearn:
  from sklearn.datasets import load_breast_cancer 

  def run_command(cmd):
      #Run command, return output as string.
      output = subprocess.Popen(cmd, stdout=subprocess.PIPE, shell=True).communicate()[0]
      return output.decode("ascii")

  def list_available_gpus():
      #Returns list of available GPU ids.
      output = run_command("nvidia-smi -L")
      # lines of the form GPU 0: TITAN X
      gpu_regex = re.compile(r"GPU (?P<gpu_id>\d+):")
      result = []
      for line in output.strip().split("\n"):
          m = gpu_regex.match(line)
          assert m, "Couldnt parse " + line
          result.append(int(m.group("gpu_id")))
      return result

  def gpu_memory_map():
      #Returns map of GPU id to memory allocated on that GPU.
      output = run_command("nvidia-smi")
      gpu_output = output[output.find("GPU Memory"):]
      # lines of the form
      # |    0      8734    C   python                                       11705MiB |
      memory_regex = re.compile(r"[|]\s+?(?P<gpu_id>\d+)\D+?(?P<pid>\d+).+[ ](?P<gpu_memory>\d+)MiB")
      rows = gpu_output.split("\n")
      result = {gpu_id: 0 for gpu_id in list_available_gpus()}
      for row in gpu_output.split("\n"):
          m = memory_regex.search(row)
          if not m:
              continue
          gpu_id = int(m.group("gpu_id"))
          gpu_memory = int(m.group("gpu_memory"))
          result[gpu_id] += gpu_memory
      return result

  def pick_gpu_lowest_memory():
      #Returns GPU with the least allocated memory
      memory_gpu_map = [(memory, gpu_id) for (gpu_id, memory) in gpu_memory_map().items()]
      best_memory, best_gpu = sorted(memory_gpu_map)[0]
      return best_gpu

  def pick_free_gpus(num_gpus=1):
      #Returns free GPUs with the least allocated memory

      memory_gpu_map = [(memory, gpu_id) for (gpu_id, memory) in gpu_memory_map().items()]
      sorted_list = sorted(memory_gpu_map)
      gpu_list = []
      for i in range(num_gpus):
          if sorted_list[i][0] == 0:
              gpu_list.append(sorted_list[i][1])
          else:
              print(f'Currently fewer than {num_gpus} GPUs are free right now, choose {i} or fewer GPUs')
              exit()
      return ','.join(map(str, gpu_list))

  def gpus_details():
      output = run_command("nvidia-smi")
      return output

  if __name__ == "__main__":
      print("-----------------Welcome -----------------")
      num_gpus = 1
      os.environ["CUDA_VISIBLE_DEVICES"] = pick_free_gpus(num_gpus)

      tf.config.optimizer.set_jit(True)  # Enable XLA.
      session = tf.compat.v1.Session(config=tf.compat.v1.ConfigProto(log_device_placement=True, gpu_options=tf.compat.v1.GPUOptions(allow_growth=True)))
      gpus = tf.config.experimental.list_physical_devices('GPU')
      if gpus:
      # Restrict TensorFlow to only use the GPUs selected
          try:
              for gpu in gpus:
                  tf.config.experimental.set_memory_growth(gpu, True)
              tf.config.experimental.set_visible_devices(gpus, 'GPU')
              logical_gpus = tf.config.experimental.list_logical_devices('GPU')
              print(len(gpus), "Physical GPUs,", len(logical_gpus), "Logical GPUs")
          except RuntimeError as e:
          # Visible devices must be set before GPUs have been initialized
              print(e)

      if gpus:
             with tf.device(tf.test.gpu_device_name()):
                 # simple binary classification task
                 data=sklearn.datasets.load_breast_cancer()

                 print('These are the Feature Names:',data.feature_names)
                 print('Binary Classification -> Target Names:',data.target_names)

                 X, y = load_breast_cancer(return_X_y=True)
                 #splitting train and test samples: I choose 20% test and 80% train
                 X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2,random_state=0)

                 def objective(trial):
                       param = {}      
                       #param['silent']      = True 
                       param['objective']   = 'binary:logistic' # objective function
                       param['eval_metric'] = ['auc','error','rmse','logloss'] # evaluation metric for cross validation
                       param['eta'] = trial.suggest_loguniform('eta', 0.001, 0.01)
                       param['max_depth'] = trial.suggest_int('max_depth', 3, 10)
                       param['subsample'] = trial.suggest_uniform('subsample', 0.7, 0.95)
                       param['n_estimators']= trial.suggest_int('n_estimators', 50, 500)
                       param['min_child_weight']= trial.suggest_int('min_child_weight', 1, 10)
                       param['gamma'] = trial.suggest_loguniform('gamma', 1e-8, 1.0)
                       param['colsample_bytree'] = 1#trial.suggest_uniform('colsample_bytree', 0.7, 1)
                       param['max_delta_step']=trial.suggest_int('max_delta_step', 1, 10)
                       param['tree_method'] = 'gpu_hist'
                       num_trees = trial.suggest_int('num_trees', 500, 10e+3)
                       #batch_size = trial.suggest_int('batch_size', 32, 130) #batch size is an important hyperparameter to tune

                       #early stopping refers to the last eval metric specified, in this case logloss
                       earlyStop=0.15*num_trees

                       #Create Train and Test Matrix
                       train = xgb.DMatrix(data=X_train,label=y_train,feature_names=data.feature_names)
                       test = xgb.DMatrix(data=X_test,label=y_test,feature_names=data.feature_names)                     

                       start=time.time()
                       booster=xgb.train(param,train,num_boost_round=num_trees,verbose_eval=100,evals=[(train,'dtrain'), (test,'dtest')],early_stopping_rounds=earlyStop)#,evals_result=evals_result)
                       end=time.time()
                       TrainingTime=end-start
                       print('Train time per interaction:',np.round(TrainingTime/num_trees,3),'seconds')

                       predictions_test = booster.predict(test)
                       predictions_train= booster.predict(train)

                       fpr_train, tpr_train, _ = sklearn.metrics.roc_curve(tar_tr,  predictions_train)
                       auc_train = sklearn.metrics.auc(fpr_train, tpr_train)

                       fpr_test, tpr_test, _ = sklearn.metrics.roc_curve(tar_ge,  predictions_test)
                       auc_test = sklearn.metrics.auc(fpr_test, tpr_test)
                       print(f"ROC curve, AUC=(train: {auc_train:.4f}, test: {auc_test:.4f})")
                       return auc_test #This is the objective function of optuna

  #Folder where you want to save the plots
  folderBDT="./BDTPlots/"

  #name associated to this study
  name="AnExample" 

  study = optuna.create_study(sampler=TPESampler(), direction="maximize") #I want to maximize the objective function
  study.optimize(objective, n_trials=1000, gc_after_trial=True) 
  trial = study.best_trial
  print("Best Score: ", trial.value)
  print("Best Params: ")

  #Thus is a csv file with the best hyperparameters found by Optuna
  for key, value in trial.params.items():
      print("  {}: {}".format(key, value))
      with open(folderBDT + 'hyperparam_optim_'+name+'.csv', 'a') as f_object:
          # Pass the file object and a list of column names to DictWriter() 
          writer_object = writer(f_object) # You will get a object of DictWriter
          writer_object.writerow([key, value])
          # Close the file object
          f_object.close()

  #Some Plots
  fig2 = optuna.visualization.matplotlib.plot_param_importances(study)
  #fig2.figure.set_size_inches(10, 8)
  fig2.figure.savefig(folderBDT+'Param_importance_'+name+'.pdf')
  fig3 = optuna.visualization.matplotlib.plot_optimization_history(study)
  #fig3.figure.set_size_inches(10, 8)
  fig3.figure.savefig(folderBDT+'History_optimization_'+name+'.pdf')
