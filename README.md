Siamese Network for Few-Shot Learning on ADNI Dataset
🧠 Project Overview
This project implements a Siamese Neural Network for Few-Shot Learning (FSL) on the Alzheimer's Disease Neuroimaging Initiative (ADNI) dataset. The primary goal is to achieve high classification accuracy on imbalanced or limited training data by leveraging pairwise similarity learning.

🔍 Problem Statement
Standard deep learning models struggle when data is scarce or classes are imbalanced. To overcome this, we use a Siamese Network that learns to compare images, rather than classify them independently. This method is effective for medical datasets like ADNI, where acquiring large labeled samples is challenging.

📁 Dataset
Source: ADNI (Alzheimer's Disease Neuroimaging Initiative)

Classes:

AD (Alzheimer's Disease)

CN (Cognitively Normal)

MCI (Mild Cognitive Impairment)

Input Shape: 128x128 grayscale images (converted to 3-channel RGB for MobileNetV2 compatibility)

Data Format: Folder structure per class

🧠 Model Architecture
A Siamese Network architecture was implemented using MobileNetV2 as the backbone for feature extraction.

Key Features:
Backbone: MobileNetV2 (from scratch, weights=None)

Input: Pairs of images

Output: Softmax over 3 classes

Pairing Strategy:

Each anchor image is paired with:

A positive sample (same class)

A negative sample (different class)

The labels for each pair are based on the anchor image.

This ensures consistency during training and correct label propagation through the loss function.

All pairs are shuffled randomly to avoid order bias.

⚙️ Implementation Details
Framework: TensorFlow 2.x / Keras

Loss Function: Categorical Crossentropy

Optimizer: Adam

Epochs: 80

Batch Size: 16

Validation Split: 15% of training data (stratified on anchor labels)

📈 Training Results
The Siamese network showed steady improvement in validation accuracy after ~20 epochs:

Epoch	Accuracy	Loss	Val Accuracy	Val Loss
1	0.46	1.10	0.33	1.09
25	0.87	0.32	0.71	0.77
50	0.95	0.13	0.75	0.76
80	1.00	0.00	0.87	0.37

✅ Evaluation Metrics
Test Accuracy: 86.78%

Evaluation Strategy:

Image pairs are evaluated by predicting the class of the anchor.

Accuracy, Precision, Recall, and F1-score are calculated based on anchor labels.

Confusion Matrix and Classification Report are computed accordingly.

markdown
Copy
Edit
              precision    recall  f1-score   support

          AD       0.89      0.85      0.87       587
          CN       0.87      0.85      0.86       604
         MCI       0.84      0.91      0.87       609

    accuracy                           0.87      1800
   macro avg       0.87      0.87      0.87      1800
weighted avg       0.87      0.87      0.87      1800
ROC Curve and Precision-Recall Curve plotted per class.
