# 3D Breast Cancer Segmentation using MRI and nnU-Net

This repository presents a complete deep learning pipeline for **3D breast cancer segmentation** using volumetric MRI data and the **nnU-Net architecture**. It leverages the BreastDM dataset to identify tumor regions with high spatial precision in the subtraction (SUB2) modality.

---

## Project Structure

```bash
.
├── 1_dataprep_&_preprocessing.ipynb              # Data loading, normalization, padding
├── 2_training.ipynb                              # 3D nnU-Net model training (PyTorch)
├── 3_inference.ipynb                             # Inference on test samples
├── 4_postprocessing_visualization_evaluation.ipynb  # Postprocessing, visualization, evaluation
├── sample_output/                                # (Optional) Small sample predictions for quick testing
└── README.md

```
## Dataset: BreastDM

- **Patients**: 262
- **Modalities** per patient:
  - `SUB2.npy`: Subtraction image (used for model training)
  - `VIBRANT.npy`, `VIBRANT+C2.npy`: Not used in this project
- **Format**: 3D `.npy` volumes of shape `(H, W, D)`
- **Mask**: Binary ground truth masks for tumor regions
- **Data Splits**: `train/`, `val/`, and `test/` (each with `images/` and `labels/` subfolders)

> Input tensors are padded and reshaped to fixed shapes like `(8, 3, 369, 369)` or `(6, 3, 369, 369)`.

---

## Model Overview: nnU-Net (3D)

The model is a 3D implementation of the popular nnU-Net framework. Key features:

- Fully convolutional 3D segmentation architecture
- Automatic adaptation to patch sizes and resolution
- Works directly on 3D MRI volumes (`SUB2.npy`)
- Postprocessing pipeline to enhance segmentation quality

---

## Pipeline Steps

### 1. Data Preprocessing  
 `1_dataprep_&_preprocessing.ipynb`

- Loads `SUB2.npy` volumes and their corresponding labels
- Normalizes intensities
- Pads volumes to consistent shape
- Saves preprocessed volumes to disk for model input

---

### 2. Model Training  
 `2_training.ipynb`

- Implements 3D nnU-Net using PyTorch
- Trains model on preprocessed data
- Logs metrics and saves checkpoints to Drive

---

### 3. Inference  
 `3_inference.ipynb`

- Loads trained model
- Predicts tumor masks on test samples
- Saves predictions to disk

---

### 4. Postprocessing & Evaluation  
 `4_postprocessing_visualization_evaluation.ipynb`

- Applies connected component filtering to clean predictions
- Computes:
  - Dice Score
  - Intersection over Union (IoU)
  - Sensitivity
  - Specificity
- Visualizes:
  - Ground truth vs predicted masks
  - Overlay on original slices
