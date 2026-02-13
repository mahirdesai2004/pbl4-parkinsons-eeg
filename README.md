# Reliable Parkinson’s Disease Detection from EEG

[![Conference](https://img.shields.io/badge/Conference-ICICC%202026-blue?style=for-the-badge)](https://icicc-conf.com/)
[![Publisher](https://img.shields.io/badge/Publisher-Springer-orange?style=for-the-badge&logo=springer&logoColor=white)](https://www.springer.com/)
[![Status](https://img.shields.io/badge/Status-Accepted-success?style=for-the-badge)](https://github.com/mahirdesai2004/pbl4-parkinsons-eeg)
[![Python](https://img.shields.io/badge/Python-3.10+-yellow?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=for-the-badge&logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)

> **Strict Subject-Wise Validation for Realistic Clinical Performance**

## 🚀 Experience the Project
🌐 **[View Project Website](https://mahirdesai2004.github.io/pbl4-parkinsons-eeg/)**  
*Interactive visualization of the problem statement, methodology, and results.*

---

## 📄 Abstract
This project presents a robust deep learning framework for detecting Parkinson's Disease (PD) using EEG signals. Unlike many existing studies that use subject-dependent cross-validation (leading to data leakage and inflated accuracy), this work employs a **strict Leave-One-Subject-Out (LOSO)** validation strategy. We utilize **EEGNet**, a compact convolutional neural network designed for EEG signal processing, to classify subjects as PD or Healthy Controls (HC). The model achieves realistic clinical performance estimates, highlighting the importance of proper validation methodologies in medical AI.

## 📊 Dataset
| Feature | Details |
| :--- | :--- |
| **Source** | [UCSD ds002778 (OpenNeuro)](https://openneuro.org/datasets/ds002778) |
| **Subjects** | 31 (15 PD, 16 Healthy) |
| **Data Type** | Resting-state EEG (ON medication) |
| **Channels** | 40 scalp electrodes |
| **Sampling** | 512 Hz |

## 🛠 Methodology
The pipeline consists of the following stages:

1.  **Preprocessing**: Artifact removal, filtering (1-40 Hz), and windowing (3s epochs, 50% overlap).
2.  **Model**: **EEGNet** (Lawhern et al., 2018), adapted for binary classification.
3.  **Validation**: **Leave-One-Subject-Out (LOSO)**.
    *   *Strict separation*: No data from the test subject is seen during training.
    *   Ensures reliable generalization to new patients.

## 📈 Results
Our strict subject-independent evaluation yields the following performance metrics:

### Subject-Level Metrics
| Metric | Score | vs Baseline |
| :--- | :--- | :--- |
| **Balanced Accuracy** | **74.58%** | *+3.12%* |
| **AUC** | **0.7875** | *+0.13* |
| **Sensitivity** | **86.67%** | *-* |
| **Specificity** | **62.50%** | *-* |

<p align="center">
  <img src="figures/confusion_matrix.png" width="45%" alt="Confusion Matrix">
  <img src="figures/roc_eegnet.png" width="45%" alt="ROC Curve">
</p>

## 📂 Repository Structure
```bash
├── code/
│   ├── 01_data_preprocessing.ipynb   # Initial data cleaning
│   └── 02_train_loso_eegnet.ipynb    # EEGNet training (LOSO)
├── figures/                          # Plots & Visualizations
├── results/                          # CSV Metrics & Logs
├── EEGNet_LOSO/                      # Model Checkpoints
├── index.html                        # Project Website
└── requirements.txt                  # Dependencies
```

## 💻 How to Run

### 1. Installation
```bash
git clone https://github.com/mahirdesai2004/pbl4-parkinsons-eeg.git
cd pbl4-parkinsons-eeg
pip install -r requirements.txt
```

### 2. Execution
*   **Preprocessing**: Run `code/01_data_preprocessing.ipynb` to generate dataset files.
*   **Training**: Run `code/02_train_loso_eegnet.ipynb` to train the model using LOSO cross-validation.

## 📝 Citation
This paper has been accepted at the **9th International Conference on Innovative Computing and Communication (ICICC-2026)**.

*   **Organized by**: Shaheed Sukhdev College of Business Studies, University of Delhi.
*   **Proceedings**: To be published in **Springer LNNS Series** (Lecture Notes in Networks and Systems).

> Citation details will be updated here upon publication of the proceedings.

---
*Manipal University Jaipur, Department of Computer Science & Engineering.*
