# 📂 X-Ray Synthetic Data Study - Notebooks

This directory contains the experimental notebooks used to generate synthetic medical images, validate their quality, and train downstream classifiers to solve the class imbalance (scarcity) problem.

## Notebook Index & Workflow

The notebooks are numbered to represent the sequential workflow.

### 1. `metadata.ipynb`
* **Purpose:** Filtered the original 15-class dataset down to 5 target classes and analyzed the class distribution.
* **Key Steps:**
    * Filtered the 15-class dataset down to 5 target categories.
    * Calculated the image distribution per class.
* **Result:** Established the final dataset composition and quantified the exact scarcity of the minority classes.
### 2. `data-seperation.ipynb`
* **Purpose:** Created a localized, high-density dataset by physically extracting images corresponding to the 5 target classes identified in the metadata analysis.
* **Key Steps:**
    * Imported the filtered CSV generated in the previous step to serve as the master manifest.
* **Result:** A streamlined, standalone dataset containing only the 5 classes of interest, significantly reducing storage overhead and accelerating training I/O.
### 3. `train-val-test-split.ipynb`
* **Purpose:** Splitted the dataset into 3 parts for training, validation and test.
* **Key Steps:**
    * Performed a **stratified split** to ensure the class distribution (of the 5 target diseases) remains consistent across all partitions.
* **Result:** Three distinct, statistically balanced dataset partitions with non-overlapping patient IDs, ensuring zero data leakage for robust model evaluation.
### **4. `train.ipynb`**
* **Purpose:** Implements a training pipeline using the **EVA-02** Vision Transformer, specifically tuned for high-resolution chest X-ray classification.
* **Key Strategy:**
    * **Architecture:** Uses `eva02_base_patch14_448` (pre-trained on ImageNet-22k/1k) processing images at **448×448** resolution to capture subtle lung opacities.
    * **Advanced Optimization:**
        * **Layer-wise Learning Rate Decay (LLRD):** Assigns lower learning rates to the backbone and higher rates to the head to preserve pre-trained features.
        * **Focal Loss + BCE:** Replaces standard Cross Entropy with **Focal Loss** ($\gamma=2$) to force the model to focus on hard-to-classify examples (minority classes).
        * **Mixed Precision (AMP):** Utilizes FP16 gradient scaling to fit the heavy EVA-02 model into memory.
    * **Robustness & Generalization:**
        * **Strong Augmentations:** Applies a rigorous mix of geometric (affine, rotation) and photometric (brightness, contrast) distortions.
        * **Exponential Moving Average (EMA):** Maintains a shadow copy of weights (decay=0.999) for stability.
        * **Model Soup:** Implements checkpoint averaging (Epoch 5 + Epoch 6) to create a final "Super Model" that generalizes better than any single epoch.
* **Output:** Saves the final averaged model as `eva_x_final_soup.pth`.
### **Acknowledgements**
* **Training Strategy:** The "EVA-X" training recipe (EVA-02, 448px, LLRD, Checkpoint Averaging) is adapted from the winning solution of a Kaggle Competition by masry1**. Their repository provided the foundation for the LLRD and Model Soup implementation used in this project.

---
