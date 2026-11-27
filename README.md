# Retinal cGAN for Diabetic Retinopathy

**Class-Conditional Generative Adversarial Networks for Synthetic Retinal Fundus Images and Minority-Class Augmentation in Diabetic Retinopathy Grading**

AI4009 Generative AI, Fall 2026, FAST-NUCES Karachi
- 23K-0021 Kirsh Kumar
- 23K-0775 Manmohan

## Overview
A class-conditional GAN generates 64×64 retinal fundus images for diabetic retinopathy grades 0 (No DR), 2 (Moderate) and 4 (Proliferative). The synthetic images are evaluated for fidelity, diversity, class consistency and memorisation. They are also used to augment a ResNet-18 grading classifier, which is compared against a conditional VAE, oversampling and classical augmentation.

## Repository layout
```
notebooks/   Google Colab notebooks (run in order)
dataset/     processed data + download instructions
paper/       research papers followed
report/      final project report
proposal/    project proposal
results/     figures and tables
```

## Dataset
APTOS 2019 Blindness Detection (Kaggle): https://www.kaggle.com/competitions/aptos2019-blindness-detection

## Papers
- Pakdelmoez et al. (2024). *Controllable retinal image synthesis using conditional StyleGAN and latent space manipulation for improved diagnosis and grading of diabetic retinopathy.* arXiv:2409.07422 (`paper/2409.07422v1.pdf`)
- Zhou et al. *DR-GAN: Conditional Generative Adversarial Network for Fine-Grained Lesion Synthesis on Diabetic Retinopathy Images.* arXiv:1912.04670 (`paper/1912.04670v3.pdf`)

*Work in progress.*
