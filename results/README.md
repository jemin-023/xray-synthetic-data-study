# Research Results & Evaluation Metrics

This directory contains the visual and statistical evidence regarding the performance of the **EVA-X (EVA-02)** model on the test dataset.

## 📊 File Descriptions

### 1. `confusion_matrix_before.png`
* **Description:** A normalized confusion matrix showing the percentage of correct and incorrect predictions for each class.
* **Key Insight:** Highlights the "Accuracy Trap" where minority classes (like *Cardiomegaly*) are frequently misclassified as the majority class (*Lung Opacity*), demonstrating the impact of class imbalance on model recall.

### 2. `roc_curves_before.png`
* **Description:** Receiver Operating Characteristic (ROC) curves for all 5 pathology classes.
* **Key Insight:** Demonstrates the model's high discriminative power (AUC scores between **0.83** and **0.98**), proving that the model has successfully learned the feature representations despite the calibration issues seen in the confusion matrix.
---
