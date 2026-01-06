# X-Ray Synthetic Data Study: Diffusion Transformers

<div align="center">

![Status](https://img.shields.io/badge/Status-Active_Research-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)
![Arch](https://img.shields.io/badge/Arch-DiT_(Diffusion_Transformer)-orange?style=for-the-badge)

</div>

---

## 📋 Overview

**xray-synthetic-data-study** is a research initiative evaluating the efficacy of **Diffusion Transformers (DiT)** for generating high-fidelity synthetic chest X-rays.

While traditional GANs often suffer from mode collapse and training instability, Diffusion Models—specifically those leveraging Transformer backbones—offer superior scalability and sample quality. This repository explores whether synthetic data generated via DiT can effectively augment real-world medical datasets to address scarcity and class imbalance in disease classification tasks.

## 🎯 Objectives

1.  **Architecture Implementation:** Train a **Diffusion Transformer (DiT)** (replacing the standard U-Net backbone) to model the complex distribution of chest X-ray data.
2.  **Latent Space Modeling:** Utilize a VAE (Variational Autoencoder) to compress X-rays into latent patches for efficient training.
3.  **Downstream Evaluation:** Train classifiers (e.g., ResNet/ViT) on synthetic-augmented datasets to benchmark performance gains against real-only baselines.
4.  **Privacy Preservation:** Assess the potential of DiT-generated data to serve as a privacy-compliant proxy for sensitive patient records.

## 🛠️ Methodology

### 1. Latent Compression

Instead of operating in pixel space, we first train (or fine-tune) a VAE to compress 256x256 X-rays into lower-dimensional latent representations.

This allows the diffusion model to focus on semantic structure rather than high-frequency noise.

### 2. Diffusion Transformer (DiT)

We employ a **transformer-based backbone** for the denoising process:

* **Patchify:** Latents are tokenized into sequences of patches.
* **Transformer Blocks:** Standard multi-head self-attention mechanisms process the noisy patches.
* **Conditioning:** Class labels (e.g., *Pneumonia*, *Normal*) are injected via adaptive layer normalization (adaLN).

### 3. Training & Sampling

* **Forward Process:** Gradually add Gaussian noise to latent patches.
* **Reverse Process:** The DiT predicts the noise to reconstruct the clean latent, which is then decoded back to pixel space.
