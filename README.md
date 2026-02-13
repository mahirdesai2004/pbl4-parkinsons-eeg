# Reliable Parkinson’s Disease Detection from EEG using Strict Subject-Wise Validation

## Abstract
This project presents a robust deep learning framework for detecting Parkinson's Disease (PD) using EEG signals. Unlike many existing studies that use subject-dependent cross-validation (leading to data leakage and inflated accuracy), this work employs a **strict Leave-One-Subject-Out (LOSO)** validation strategy. We utilize **EEGNet**, a compact convolutional neural network designed for EEG signal processing, to classify subjects as PD or Healthy Controls (HC). The model achieves realistic clinical performance estimates, highlighting the importance of proper validation methodologies in medical AI.

**Conference Paper Accepted at ICICC 2026.**

## Dataset
*   **Source**: [UCSD ds002778 (OpenNeuro)](https://openneuro.org/datasets/ds002778/versions/1.0.4)
*   **Subjects**: 31 total (15 Parkinson’s Disease, 16 Healthy Controls)
*   **Data Type**: Resting-state EEG (ON medication for PD subjects)
*   **Channels**: 40 scalp electrodes
*   **Sampling Rate**: 512 Hz

## Methodology
The pipeline consists of the following stages:
1.  **Preprocessing**: Artifact removal, filtering (1-40 Hz), and windowing (3-second epochs with 50% overlap).
2.  **Model**: **EEGNet** (Lawhern et al., 2018), adapted for binary classification.
    *   Temporal Convolution
    *   Depthwise Spatial Convolution
    *   Separable Convolution
3.  **Validation**: **Leave-One-Subject-Out (LOSO)**.
    *   For each fold, one subject is held out completely for testing.
    *   The model is trained on the remaining 30 subjects.
    *   This process is repeated for all 31 subjects to ensure no data leakage.

## Results
Our strict subject-independent evaluation yields the following performance metrics:

| Metric | Score |
| :--- | :--- |
| **Balanced Accuracy** | **74.58%** |
| **AUC (Area Under Curve)** | **0.7875** |
| **Sensitivity** | 86.67% |
| **Specificity** | 62.50% |

*Comparison*: This approach outperforms a baseline Bandpower + SVM model (Balanced Accuracy: 71.46%) while providing more reliable generalization estimates than subject-dependent methods.

## Repository Structure
```
├── code/
│   ├── 01_data_preprocessing.ipynb   # Initial data cleaning and windowing
│   └── 02_train_loso_eegnet.ipynb    # EEGNet training with LOSO validation
├── figures/                          # Project visualization and plots
│   ├── confusion_matrix.png
│   ├── roc_eegnet.png
│   └── ...
├── results/                          # Output metrics and logs
│   ├── RESULTS_comparison_table.csv
│   └── ...
├── EEGNet_LOSO/                      # (Git-ignored) Model checkpoints and logs
├── ML_BASELINE/                      # (Git-ignored) Baseline model artifacts
├── index.html                        # GitHub Pages deployment
├── requirements.txt                  # Python dependencies
└── README.md                         # Project documentation
```

## How to Run

### 1. Installation
Clone the repository and install the required dependencies:
```bash
git clone https://github.com/mahirdesai2004/pbl4-parkinsons-eeg.git
cd pbl4-parkinsons-eeg
pip install -r requirements.txt
```

### 2. Data Preparation
*   Download the dataset from [OpenNeuro (ds002778)](https://openneuro.org/datasets/ds002778) and place it in the project root (or update paths in notebooks).
*   Run the preprocessing notebook:
    `code/01_data_preprocessing.ipynb`
    *   This will generate `X.npy`, `y.npy`, and `groups.npy`.

### 3. Training & Evaluation
*   Run the training notebook:
    `code/02_train_loso_eegnet.ipynb`
    *   This will execute the LOSO validation loop.
    *   Results and checkpoints will be saved locally.

## Reproducibility Note
*   **Random Seed**: We fix random seeds for NumPy and TensorFlow to ensure consistent results.
*   **Hardware**: Training can be performed on a standard CPU or GPU (recommended).
*   **Data Exclusion**: To comply with privacy and storage limits, raw EEG data (`.npy`) and trained model weights (`.h5`) are excluded from this repository.

## Citation
If you use this code or methodology, please cite our paper:

> **[Author Names]**. "Reliable Parkinson’s Disease Detection from EEG using Strict Subject-Wise Validation." *International Conference on IoT, Communication and Coding (ICICC)*, 2026.

---
*Manipal University Jaipur, Department of Computer Science & Engineering.*
