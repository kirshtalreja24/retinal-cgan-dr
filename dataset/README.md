# Dataset

**Source:** APTOS 2019 Blindness Detection (Kaggle):
https://www.kaggle.com/competitions/aptos2019-blindness-detection
(3,662 labelled fundus photographs; grades 0–4.)

The raw download (~10 GB) is not stored here. `notebooks/01_data_preprocessing.ipynb` downloads it
with the Kaggle API and produces the processed files below.

## Files
| File | Contents |
|---|---|
| `aptos_64.npz` | `images` (uint8, N×64×64×3), `labels` (0/1/2), `grades` (0/2/4), `id_codes`, `split` (`train`/`val`/`test`/`excluded`) |
| `splits.csv` | `id_code`, `grade`, `label`, `split` for every image |

## Processing
- Kept grades **0 (No DR)**, **2 (Moderate)** and **4 (Proliferative)** → labels 0, 1, 2.
- Cropped the black border, padded to square, resized to 64×64, applied a circular field-of-view mask.
- Stratified 70 / 15 / 15 train / val / test split (seed 42).
- Leakage check: val/test images whose high-pass detail correlation with any training image was ≥ 0.90
  were marked `excluded` (77 images).

| Split | Grade 0 | Grade 2 | Grade 4 |
|---|---|---|---|
| train | 1263 | 699 | 207 |
| val | 262 | 120 | 39 |
| test | 264 | 127 | 41 |

The data is used under the Kaggle competition rules, for academic purposes only.
