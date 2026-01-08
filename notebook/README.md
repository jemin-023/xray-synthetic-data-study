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
---
