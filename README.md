# Optimizing Deep Learning Models for Accurate & Robust Medical Image Segmentation
*Project completed during a Winter Internship at NIT Rourkela*

<p align="center">
  <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white"></a>
  <a href="https://pytorch.org/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white"></a>
  <a href="https://lightning.ai/"><img alt="PyTorch Lightning" src="https://img.shields.io/badge/Lightning-792EE5?logo=lightning&logoColor=white"></a>
  <a href="https://github.com/qubvel/segmentation_models.pytorch"><img alt="segmentation-models-pytorch" src="https://img.shields.io/badge/segmentation--models--pytorch-smp-2F855A"></a>
  <a href="./med-seg.ipynb"><img alt="Made with Jupyter" src="https://img.shields.io/badge/Made%20with-Jupyter-F37626?logo=jupyter&logoColor=white"></a>
  <a href="./LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-000000.svg"></a>
</p>

> Reproducible PyTorch Lightning pipeline for medical image segmentation (Kvasir-SEG), 
> with strong training setup, clear metrics (Dice/IoU, ROC-AUC, PR-AUC), and clean qualitative panels.

## Highlights

- **Task:** Medical Image Segmentation on **Kvasir-SEG** (polyps) with strong quantitative + qualitative evaluation.
- **Model:** `UNet(resnet34 encoder)` via `segmentation_models_pytorch`.
- **Training:** PyTorch Lightning (`mixed-precision`, `AdamW`, cosine LR schedule, early stopping, checkpoints).
- **Augmentations:** Resize → HorizontalFlip → ShiftScaleRotate → Brightness/Contrast → GaussNoise → Normalize (Albumentations).
- **Metrics & Analysis:** Dice & IoU (per-image + aggregate), ROC–AUC, PR–AUC, threshold sweeps, calibration (ECE), coverage vs Dice, best/worst/random panels.
- **Reproducibility:** All steps kept inside `med-seg.ipynb`; outputs auto-saved to `outputs/` as figures and overlays.

## Repo Map
```
medical-image-segmentation-nitr-winter24/
├─ med-seg.ipynb # main, reproducible notebook
├─ figures/ # exported plots & panels (for README/gallery)
├─ reports/ # (placeholder for pdfs/notes if needed)
├─ data/ # (optional) local samples / CSV splits
├─ src/ # (optional) helper scripts (future growth)
├─ README.md # you are here
└─ LICENSE # MIT
```
## Dataset & Preprocessing

**Dataset:** [Kvasir-SEG] — 1,000 gastrointestinal polyp images with expert-annotated masks (binary segmentation). Images vary from ~332×487 to 1920×1072.  

**How the notebook gets data**
- Tries to detect Kvasir-SEG under `/kaggle/input/…`.
- If missing, downloads `kvasir-seg.zip` and unzips to `/kaggle/working/medseg/data/Kvasir-SEG/`.
- Auto-detects `images/` and `masks/` folders and verifies counts.

**Pairs & splits (CSV)**
- Pairs image↔mask by stem into `pairs.csv`.
- Computes a simple mask **coverage** (% of positive pixels) and a boolean **has_polyp**.
- Creates stratified **train/val** CSVs (`train.csv`, `val.csv`) while preserving the has_polyp distribution.

**Augmentations & normalization (Albumentations)**
- `Resize(256, 256)`
- `HorizontalFlip(p=0.5)`, `RandomRotate90(p=0.25)`
- `ShiftScaleRotate(shift_limit=0.02, scale_limit=0.1, rotate_limit=15, border_mode=REFLECT_101, p=0.4)`
- `RandomBrightnessContrast(p=0.3)`, `GaussNoise(var_limit=(5, 20), p=0.2)`
- `Normalize(mean=(0.485,0.456,0.406), std=(0.229,0.224,0.225))`
- `ToTensorV2()`

**Validation preprocessing**
- `Resize(256, 256)` → `Normalize` → `ToTensorV2()` (no heavy augs)

**Directory layout (after setup)**

