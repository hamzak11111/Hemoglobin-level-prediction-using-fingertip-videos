# Non-Invasive Hemoglobin Level Prediction from Fingertip Videos

This repository contains our work on predicting hemoglobin (Hb) levels
using fingertip video recordings. We build upon the dataset and baseline
model from the research paper **"Fingertip Video Dataset for
Non-Invasive Diagnosis of Anemia Using ResNet-18 Classifier"**, and
propose efficient preprocessing and multiple deep-learning
architectures, including a hybrid CNN--LSTM model.

## Dataset

-   130 training samples, 30 testing samples\
-   Each sample: 1-minute fingertip video\
-   Ground-truth Hb levels included via CSV\
-   Dataset split provided by original authors

## Preprocessing Pipeline

1.  Sample N equidistant frames (N = 5, 10, 15)\
2.  Center crop to 224×224×3\
3.  Normalize channels\
4.  Stack frames into a single tensor

This is significantly more efficient than the paper's 1800-frame
extraction method.

## Models Implemented

-   **ResNet-18** (pretrained)\
-   **VGG16** (pretrained)\
-   **EfficientNet** (pretrained)\
-   **Hybrid ResNet18--LSTM**

### CNN Model Flow

1.  Extract CNN embeddings for each frame\
2.  Concatenate\
3.  Fully connected regression head

### Hybrid ResNet18--LSTM

1.  Extract CNN embeddings\
2.  Feed sequence into 2-layer LSTM\
3.  Final hidden state → regression head

## Training Settings

  Parameter    Value
  ------------ ---------------------
  Frames       5, 10, 15
  Epochs       10
  Batch size   8
  LR           1e-4
  Loss         MSE
  Optimizer    Adam (weight decay)
  Hardware     Kaggle T4 GPU

Total experiments: **12**

## Results Summary

-   ResNet-18 showed best overall performance\
-   LSTM model did not benefit from additional frames\
-   EfficientNet and VGG16 performed variably

## Comparison With Research Paper

Our ResNet-18 (15 frames) achieved: - **RMSE Train:** 0.70\
- **RMSE Test:** 1.42\
- **Model Size:** 44.62 MB

Comparable performance to the paper while requiring far fewer frames and
less compute.

## Contributions

-   Lightweight preprocessing pipeline\
-   Benchmarking multiple CNNs\
-   Hybrid CNN--LSTM model\
-   Strong performance with small model size

## Future Work

-   Incorporate 3D CNNs\
-   Temporal transformers\
-   Real-time deployment
