# Histopathology Image Classification

## Project Overview

This project focuses on multi-class classification of histopathology images of colorectal tissue.

The project investigates how different feature extraction methods and classifiers affect image classification performance. The main goal is to compare classical and deep-learning-based feature representations and identify the approach that provides the strongest generalization performance.

The project was developed as part of the Machine Learning course in the Department of Digital Medical Technologies at HIT – Holon Institute of Technology.

## Dataset

The project uses the **Kather Texture 2016** dataset, containing 5,000 histopathology image tiles divided into 8 tissue classes.

Each image has a size of **150 × 150 × 3**.

The eight classes are:

- 01_TUMOR
- 02_STROMA
- 03_COMPLEX
- 04_LYMPHO
- 05_DEBRIS
- 06_MUCOSA
- 07_ADIPOSE
- 08_EMPTY

The dataset was divided using an **80/20 stratified train-test split**:

- Training set: 4,000 images
- Test set: 1,000 images
- 500 training images and 125 test images per class

The dataset itself is not included in this repository.

## Project Pipeline

The project consists of the following main stages:

1. Dataset preparation and metadata creation
2. Exploratory Data Analysis (EDA)
3. Train-test split
4. Feature extraction
5. Feature normalization
6. t-SNE visualization
7. Nine classification experiments
8. Comparison of the nine experiments
9. Final improvement experiment using EfficientNetB0

## Feature Extraction Methods

Three feature extraction approaches were evaluated.

### 1. Downsample + Flatten

The original images were resized from **150 × 150** to **32 × 32** pixels and then flattened into a 3,072-dimensional feature vector.

### 2. PCA

The original 67,500-dimensional image representation was reduced to **256 principal components** using Principal Component Analysis (PCA).

### 3. VGG16

A pretrained **VGG16** network with ImageNet weights was used as a feature extractor.

The convolutional features were flattened into an **8,192-dimensional** representation and subsequently normalized using StandardScaler.

## Classification Experiments

The first nine experiments evaluated all combinations of the three feature extraction methods and three classifiers:

| Feature Extraction | SVM | Softmax | Neural Network |
|---|---:|---:|---:|
| Downsample + Flatten | ✓ | ✓ | ✓ |
| PCA | ✓ | ✓ | ✓ |
| VGG16 Backbone | ✓ | ✓ | ✓ |

The Neural Network used a hidden Dense layer followed by a Softmax output layer.

Performance was evaluated using:

- Training Accuracy
- Test Accuracy
- Training Macro F1
- Test Macro F1
- Overfitting Gap
- Test Confusion Matrix

For the Softmax and Neural Network experiments, training curves for Accuracy and Loss were also examined.

## Results – Nine Basic Experiments

The main results were:

| Experiment | Test Accuracy | Test Macro F1 |
|---|---:|---:|
| Downsample + Flatten + SVM | 0.706 | 0.7057 |
| PCA + SVM | 0.596 | 0.5942 |
| VGG16 + SVM | 0.842 | 0.8427 |
| Downsample + Flatten + Softmax | 0.487 | 0.4643 |
| PCA + Softmax | 0.474 | 0.4608 |
| VGG16 + Softmax | 0.879 | 0.8789 |
| Downsample + Flatten + Neural Network | 0.557 | 0.5372 |
| PCA + Neural Network | 0.577 | 0.5735 |
| VGG16 + Neural Network | 0.876 | 0.8755 |

The results demonstrated that the choice of feature extraction method had a substantially larger effect on performance than the choice of classifier.

In particular, VGG16 consistently outperformed Downsample + Flatten and PCA across all three classifiers.

## Final Experiment – EfficientNetB0

After analyzing the nine basic experiments, the final experiment focused on improving the feature extraction stage rather than substantially increasing classifier complexity.

A pretrained **EfficientNetB0** model with ImageNet weights was used as a feature extractor. The resulting features were classified using a neural network with:

- Dense layer with 256 neurons
- Batch Normalization
- Dropout
- Dense layer with 64 neurons
- Batch Normalization
- Dropout
- Softmax output layer
- Adam optimizer
- Early Stopping
- ReduceLROnPlateau

### Final Performance

The final EfficientNetB0-based model achieved:

- **Test Accuracy: 91.00%**
- **Test Macro F1: 0.9192**
- **Overfitting Gap: 5.55%**

This was the strongest result obtained in the project.

The improvement supports the conclusion that, for this dataset, improving the quality of the feature representation had a greater impact than increasing the complexity of the classifier.

## Technologies

- Python
- NumPy
- Pandas
- Matplotlib
- PIL
- Scikit-learn
- TensorFlow
- Keras

## Main Concepts

The project demonstrates practical use of:

- Image preprocessing
- Stratified train-test splitting
- Feature extraction
- Dimensionality reduction
- PCA
- t-SNE
- VGG16
- EfficientNetB0
- SVM
- Softmax classification
- Neural Networks
- Batch Normalization
- Dropout
- L2 Regularization
- Early Stopping
- Learning-rate scheduling
- Macro F1 evaluation
- Confusion matrices

## Repository Contents

The main notebook contains the complete project workflow, including preprocessing, feature extraction, the nine basic experiments, comparison of results, and the final EfficientNetB0 experiment.

## Authors

**Ayelet Yehezkel**  
**Tamar Levitan**

Department of Digital Medical Technologies  
HIT – Holon Institute of Technology
