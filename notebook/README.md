# 📂 X-Ray Synthetic Data Study - Notebooks

This directory contains the experimental notebooks used to generate synthetic medical images, validate their quality, and train downstream classifiers to solve the class imbalance (scarcity) problem.

## 🎯 Objective
To evaluate if **Synthetic Data Augmentation** improves model performance on minority classes (specifically **Class 2**) compared to traditional oversampling ("xeroxing") and heavy augmentation.

## Notebook Index & Workflow

The notebooks are numbered to represent the sequential workflow.

### 1. `metadata.ipynb`
* **Purpose:** Filtered the original 15-class dataset down to 5 target classes and analyzed the class distribution.
* **Key Steps:**
    * Filtered the 15-class dataset down to 5 target categories.
    * Calculated the image distribution per class.
    * **Result:** Established the final dataset composition and quantified the exact scarcity of the minority classes..

---

## ⚠️ Critical Data Hygiene Protocols

To ensure the integrity of the study, the following rules are hard-coded into the data loaders in these notebooks:

1.  **NO Synthetic Leakage:** Synthetic images are **only** used in the Training Set.
2.  **Sacrosanct Validation:** The `Clean Val Set` and `Personal Test Set` consist of **100% Real Images**. They are never touched by the generator or the augmentation pipeline during inference.

