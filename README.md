# ML-For-Cybersecurity--Analysis-and-Evaluation-of-Backdoor-Detection-in-Cybersecurity-Models---BadNet

## ECE-GY 9163 - ML for Cyber Security, Fall 2023

### Author
Avinash Vijayarangan av3134

## Introduction

This study discusses the outcomes of Lab 4, focusing on a Pruning-Based Backdoor Detector for Neural Networks. The research explores using a pruning defense on a compromised neural network model (BadNet), trained using the YouTube Face dataset. The objective is to neutralize the backdoor without compromising the accuracy of clean data inputs. Various pruning intensities were tested to find a balance between network security and performance.

## Dataset

The YouTube Face dataset, comprising both clean and poisoned data, was utilized. The clean validation and test datasets (valid.h5 and test.h5) were used for model fine-tuning and evaluation. For backdoor attack simulations, poisoned datasets with a sunglasses trigger (bd valid.h5 and bd test.h5) were employed.

## Workflow

The study involved implementing a pruning defense strategy on a neural network. This involved selectively removing network channels based on their activation levels until the accuracy fell by predefined thresholds (2%, 4%, 10%). Using TensorFlow and Keras, the performance of pruned models was assessed against both original and poisoned data. The method aimed to maintain accuracy while effectively detecting and mitigating backdoor threats.

## Running the Code

To run this project, follow the steps below:

1. Upload the `lab4.ipynb` notebook to Google Colab or Jupyter Notebook environment.
2. Ensure the following data files are uploaded to your Google Drive:
    - BadNet weights file
    - Benign data content (`valid.h5` and `test.h5`)
    - Poisoned data content (`bd_valid.h5` and `bd_test.h5`)
3. Mount your Google Drive in the Colab notebook to access the datasets:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
4. Set the file paths in the `lab4.ipynb` notebook to match the locations of your data files in Google Drive. Replace path-in-drive with the actual path to your files:
   ```python
      clean_data_filename = '/content/drive/MyDrive/Lab3/cl/valid.h5'
      test_filename = '/content/drive/MyDrive/Lab3/cl/test.h5'
      poisoned_filename = '/content/drive/MyDrive/Lab3/bd/bd_test.h5'
      model_name = '/content/drive/MyDrive/Lab3/models/bd_net.h5'
      model_weights = '/content/drive/MyDrive/Lab3/models/bd_weights.h5'


## Results

The following table shows the accuracy and attack rate of the repaired models at different pruning thresholds:

| Model         | Repaired Clean Accuracy | Attack Rate |
|---------------|-------------------------|-------------|
| 2% Repaired   | 95.7443                 | 100         |
| 4% Repaired   | 92.1278                 | 99.9844     |
| 10% Repaired  | 84.3336                 | 77.2097     |

<img src="https://github.com/Nagharjun17/ML-for-Cybersec---Pruning-for-Backdoor-Detection-in-Neural-Nets/blob/main/data/modelcomp.png?raw=true" width="400" alt="Comparison of Repaired Clean Accuracy and Attack Rate for each pruned model">


*Figure: Comparison of Repaired Clean Accuracy and Attack Rate for each pruned model.*

The results show that as the pruning threshold increases from 2\% to 10\%, the repaired model's accuracy on clean validation data decreases. This shows that there is a trade-off between accuracy and removing the backdoor. So, the thresholding should be chosen properly.

