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
dataset/     processed data (aptos_64.npz, splits.csv) + download instructions
paper/       research papers followed
report/      final project report
proposal/    project proposal
results/     figures and tables (see results/README.md)
```

## How to run
All notebooks run on Google Colab (T4 GPU) with the project folder in Google Drive at `MyDrive/GenAI_Project`.

| Notebook | What it does | Time on T4 |
|---|---|---|
| `01_data_preprocessing` | Downloads APTOS via the Kaggle API, preprocesses to 64×64, splits, removes near-duplicates | ~15 min |
| `02_conditional_gan` | Trains the cGAN (hinge loss, spectral norm, projection D, DiffAugment, EMA, mode-seeking loss) and generates 3×3000 images | ~1.5 h |
| `03_conditional_vae` | Trains the cVAE baseline and generates 3×3000 images | ~5 min |
| `04_evaluation` | ResNet-18 experiments E1–E6 (3 seeds), FID/KID, LPIPS, class consistency, memorisation | ~30 min |

## Dataset
APTOS 2019 Blindness Detection (Kaggle): https://www.kaggle.com/competitions/aptos2019-blindness-detection

## Papers
- Pakdelmoez et al. (2024). *Controllable retinal image synthesis using conditional StyleGAN and latent space manipulation for improved diagnosis and grading of diabetic retinopathy.* arXiv:2409.07422 (`paper/2409.07422v1.pdf`)
- Zhou et al. *DR-GAN: Conditional Generative Adversarial Network for Fine-Grained Lesion Synthesis on Diabetic Retinopathy Images.* arXiv:1912.04670 (`paper/1912.04670v3.pdf`)

## Key results
| | Macro-F1 | Grade-4 recall | FID ↓ | LPIPS diversity |
|---|---|---|---|---|
| Real only (E1) | 0.768 ± 0.018 | 0.350 | – | 0.209 (real) |
| + classical aug (E2) | **0.782 ± 0.010** | **0.398** | – | – |
| + cVAE synthetic (E4) | 0.767 ± 0.019 | 0.333 | 119.2 | 0.124 |
| + cGAN synthetic (E5) | 0.749 ± 0.012 | 0.301 | **63.7** | **0.219** |

The cGAN produces clearly better and more diverse images than the cVAE (FID 63.7 vs 119.2) and does not copy
training images. At 64×64 with only 207 real grade-4 images, however, adding synthetic grade-4 images did not
improve grading; classical augmentation remained the strongest method. Full tables: [`results/README.md`](results/README.md).
