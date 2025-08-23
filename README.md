# Optimizing Deep Learning Models for Accurate & Robust Medical Image Segmentation

> Winter Internship @ **NIT Rourkela** (Dec 2024–Feb 2025). Reproducible **PyTorch Lightning** pipeline for medical image segmentation (Kvasir‑SEG), with strong training setup, clear metrics (Dice/IoU, ROC‑AUC, PR‑AUC), and clean qualitative panels.

<p align="center">
  <a href="https://www.python.org/"><img alt="Python" src="https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white"></a>
  <a href="https://pytorch.org/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-LTS-EE4C2C?logo=pytorch&logoColor=white"></a>
  <a href="https://lightning.ai/"><img alt="PyTorch Lightning" src="https://img.shields.io/badge/Lightning-2.x-792EE5?logo=lightning&logoColor=white"></a>
  <a href="https://github.com/qubvel/segmentation_models.pytorch"><img alt="segmentation‑models‑pytorch" src="https://img.shields.io/badge/segmentation--models--pytorch-0.3.x-black"></a>
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-green.svg"></a>
</p>

---

## Table of Contents
- [Project Highlights](#project-highlights)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
  - [Setup](#setup)
  - [Dataset](#dataset)
- [How It Works](#how-it-works)
  - [Architecture & Training](#architecture--training)
  - [Metrics](#metrics)
- [Results](#results)
  - [Quantitative](#quantitative)
  - [Qualitative](#qualitative)
- [Reproducing the Experiments](#reproducing-the-experiments)
- [Troubleshooting](#troubleshooting)
- [Roadmap](#roadmap)
- [Cite / Acknowledge](#cite--acknowledge)
- [License](#license)

---

## Project Highlights
- **End‑to‑end** training & evaluation for **binary medical segmentation**.
- Built on **PyTorch Lightning** for clean training loops and logging.
- Uses **segmentation‑models‑pytorch** for strong backbones & losses.
- Clear **evaluation**: Dice, IoU, ROC‑AUC, PR‑AUC; per‑image histograms and calibration checks.
- Helpful **visuals**: quick overlay sanity checks; best/worst/random galleries.

## Repository Structure
```
medical-image-segmentation-nitr-winter24/
├── data/                    # Dataset (Kvasir-SEG) or placeholder for download
├── reports/                 # Generated reports, logs, evaluation figures
│   ├── figure_03.png        # Confusion matrix (val)
│   ├── figure_04.png        # ROC curve (val)
│   ├── figure_06.png        # Per-image Dice histogram
│   └── figures/
│       ├── quick_eda_overlays.png
│       └── result_gallery.png
├── src/                     # Training & model code (Lightning modules, utils)
├── med-seg.ipynb            # Notebook: EDA → training → evaluation → plots
├── README.md                # (this file)
└── LICENSE                  # MIT
```

## Getting Started

### Setup
```bash
# 1) Clone
git clone https://github.com/git-tarik/medical-image-segmentation-nitr-winter24.git
cd medical-image-segmentation-nitr-winter24

# 2) (Recommended) create a virtual environment
python -m venv .venv
# Linux/Mac
source .venv/bin/activate
# Windows
.venv\\Scripts\\activate

# 3) Install dependencies
pip install -r requirements.txt
```

### Dataset
This project is configured for **Kvasir‑SEG** (GI polyp segmentation). Prepare the folder like below:
```
data/
└── Kvasir-SEG/
    ├── images/        # original images
    └── masks/         # corresponding segmentation masks
```
If you use a different dataset, just mirror this structure and update the config/paths accordingly.

## How It Works

### Architecture & Training
- **Backbones** from `segmentation_models_pytorch` (e.g., U‑Net/DeepLab variants), chosen for strong baselines.
- **LightningModule** handles: optimizer/criterion, train/val/test steps, metric logging.
- **Augmentation** & preprocessing are applied consistently to images and masks.
- **Checkpointing/Early‑stopping** ensure best‑val models are saved.

### Metrics
We compute both **threshold‑based metrics** (Dice, IoU) and **threshold‑free** diagnostics (ROC‑AUC/PR‑AUC). In addition, per‑image histograms surface long‑tail failure modes.

## Results

### Quantitative
<p align="center">
  <img src="reports/figure_003.png" alt="Confusion matrix (validation)" width="75%"/>
</p>
<p align="center">
  <img src="reports/figure_004.png" alt="ROC curve (validation)" width="75%"/>
</p>
<p align="center">
  <img src="reports/figure_006.png" alt="Per‑image Dice histogram" width="75%"/>
</p>

### Qualitative
<p align="center">
  <img src="reports/figures/quick_eda_overlays.png" alt="Quick EDA overlays" width="85%"/>
</p>
<p align="center">
  <img src="reports/figures/result_gallery.png" alt="Best/Worst/Random prediction gallery" width="85%"/>
</p>

> **Tip:** In the gallery, panels are grouped into **Top‑K Best**, **Worst**, and **Random** samples. Typical color code: *Green = TP*, *Yellow = FP*, *Cyan = FN*.

## Reproducing the Experiments
```bash
# Train (example; adjust flags/paths as needed)
python -m src.train \
  --data_dir data/Kvasir-SEG \
  --img_size 384 \
  --batch_size 8 \
  --max_epochs 50 \
  --model unet_resnet34 \
  --loss dice+bce \
  --lr 3e-4

# Evaluate & generate reports
python -m src.evaluate --ckpt runs/best.ckpt --data_dir data/Kvasir-SEG
```
> See `med-seg.ipynb` for an easier notebook‑driven workflow: EDA → training → evaluation → report export.

## Troubleshooting
- **CUDA out of memory:** reduce `--batch_size` or image size; enable gradient accumulation.
- **Unstable training:** try a lower learning rate; check augmentations; verify mask encoding (0/1).
- **Poor validation Dice:** re‑balance loss (e.g., Dice+CE), confirm that thresholds & post‑processing are consistent.

## Roadmap
- [ ] Add multi‑class support & class‑specific metrics.
- [ ] Release Weights & Biases/Lightning Fabric logger configs.
- [ ] Provide Dockerfile for one‑command reproducibility.
- [ ] Add Test‑Time Augmentation (TTA) and simple CRF post‑processing.

## Cite / Acknowledge
If you use this repository, please consider citing the project and the **Kvasir‑SEG** dataset. Also credit the open‑source libraries that make this work possible: **PyTorch**, **PyTorch Lightning**, and **segmentation‑models‑pytorch**.

## License
This project is released under the **MIT License**. See [LICENSE](LICENSE) for details.

