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
##  Dataset
