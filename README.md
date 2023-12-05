# ML-for-Cybersec---Pruning-for-Backdoor-Detection-in-Neural-Nets

## ECE-GY 9163 - ML for Cyber Security, Fall 2023

### Author
Nagharjun M (nm4074)

## Introduction

This report contains explanations for the findings in Lab 4 - Designing and Evaluating a Pruning-Based Backdoor Detector for Neural Networks. Pruning defence is applied to a compromised BadNet model trained on the YouTube Face dataset, aiming to disable the backdoor while preserving accuracy for clean inputs. Further findings, based on various pruning levels, provide insights into balancing network integrity with robustness against backdoor attacks.

## Dataset

The YouTube Face dataset is used in this experiment which is further divided into clean and poisoned subsets. I use clean validation and test sets (valid.h5 and test.h5) to fine-tune and assess the model. For backdoor simulation, poisoned datasets with a sunglasses trigger (bd\_valid.h5 and bd\_test.h5) are used to test the defence.

## Workflow

I implemented a pruning defense on a neural network, selectively removing channels based on activation levels until accuracy dropped by predefined thresholds (2\%, 4\%, 10\%). Using TensorFlow and Keras, I evaluated the pruned models against both original and poisoned data, classifying inputs as clean or backdoored based on model agreement. This approach aimed to balance accuracy with effective backdoor detection.

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
    cleanValidDataPath = '/content/drive/MyDrive/your-path-in-drive/valid.h5'
    cleanTestDataPath = '/content/drive/MyDrive/your-path-in-drive/test.h5'
    poisonedTestDataPath = '/content/drive/MyDrive/your-path-in-drive/bd_test.h5'
    badModelPath = '/content/drive/MyDrive/your-path-in-drive/bd_net.h5'
    badModelWeightsPath = '/content/drive/MyDrive/your-path-in-drive/bd_weights.h5'


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

