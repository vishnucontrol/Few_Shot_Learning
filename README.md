Siamese Network for Few-Shot Learning on ADNI Dataset
1. Problem Statement
Standard deep learning models often fail when:

Training data is limited

Classes are imbalanced

To address this, we use a Siamese Neural Network that learns pairwise similarity instead of directly classifying samples. This is especially useful in medical imaging (like ADNI), where labeled data is hard to obtain.

2. Dataset Description
Source: ADNI

Classes:

AD: Alzheimer’s Disease

CN: Cognitively Normal

MCI: Mild Cognitive Impairment

Image Shape: 128×128 grayscale images
(converted to 3-channel RGB to work with MobileNetV2)

Structure: Folder-per-class format for easy loading

3. Model Architecture
Base Model: MobileNetV2 (weights=None)

Siamese Setup:

Input: Pair of images

Output: Softmax across 3 classes (AD, CN, MCI)

Pairing Strategy:

Each anchor image is paired with:

A positive image (same class)

A negative image (different class)

Labels are assigned only from the anchor

Final training data is shuffled to prevent ordering bias

4. Training Configuration
Framework: TensorFlow 2.x / Keras

Loss: Categorical Crossentropy

Optimizer: Adam

Epochs: 80

Batch Size: 16

Validation Split: 15% (stratified by class)

| Epoch | Accuracy | Loss | Val Accuracy | Val Loss |
| ----- | -------- | ---- | ------------ | -------- |
| 1     | 0.46     | 1.10 | 0.33         | 1.09     |
| 25    | 0.87     | 0.32 | 0.71         | 0.77     |
| 50    | 0.95     | 0.13 | 0.75         | 0.76     |
| 80    | 1.00     | 0.00 | 0.87         | 0.37     |
