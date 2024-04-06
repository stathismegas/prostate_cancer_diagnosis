# Deep Learning model for prostate cancer diagnosis and cancer stage prediction from H&E histology images
Based on internal benchmarking we settled with DenseNet for the cancer stage prediction, and ResNet56 for the cancer/benign classification task.

# Cancer diagnosis (Cancer vs healthy classification)
Running 
```
python benign_cancerous_resnet56_final.py
```
performs the following tasks
- create matrices for the images and for the label of the train, val, test sets
- covert to categorical, normalize pixel values, and decide whether to subtract mean
- define a function that creates a DenseNet, and a function that prints the  learning rate at the end of each epoch
- perform grid search for hyperparameters
- create a t-SNE plot with PCA preprocessing
- perform manual err analysis
- save plot of confusion matrices at the tile level and the patient level.

  
# Cancer stage (Gleason Level) prediction
Running
```
python densenet_3class_cancer.py
```
implements the following pipeline
- create dictionary based on the csv file with the labels
- create matrices for train, test data
- normalize pixel values in the data and split them into train, validation and test sets
- define lr_schedule
- define ResNet layer
- define ResNetv2 architecture
- subtract mean and convert to categorical
- create function evaluate_network which has x_train, x_val as global variables, returns only the val_acc, and is solely used for the Bayesian Hyperparameter Optimization
- create function create_train_return_model, which fulfills a similar goal as evaluate_network but also retunrs the model, to do manual hyperparameter tuning 
- implement the Bayesian Hyperparameter Optimization to roughly tune the hyperparameters.
- do some further manual tuning of the Hyperparameters using the function create_train_return_model
- plot training history for best model, and evaluate on test set
- make t-SNE plots
- print statements for manual err analysis
- plot accuracy vs image size

# Manual err analysis using grad_cam_heat
grad_cam_heat.ipynb shows what features the model uses to make its prediction in one of the false positive diagnoses.


