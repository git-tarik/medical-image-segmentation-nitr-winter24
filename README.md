# Optimizing Deep Learning Models for Accurate & Robust Medical Image Segmentation
**NIT Rourkela – Winter Internship (Dec 2024 – Feb 2025)**

![Made with Jupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![NIT Rourkela](https://img.shields.io/badge/NIT%20Rourkela-Winter%20Internship-ff8c00)

> A clean, recruiter-friendly repository showcasing my medical image segmentation work completed during the Winter Internship at the **Department of Computer Science & Engineering, NIT Rourkela**.  
> The project focuses on robust training pipelines, clear evaluation (Dice/IoU), and reproducible visuals.


### Repo map
```
├─ med-seg.ipynb                        # main, reproducible notebook
├─ figures/                             # all plots auto-extracted from the notebook
├─ reports/                             # reports or artifacts (kept empty here)
├─ data/                                # (optional) small samples if you add them
├─ src/                                 # (optional) helper scripts later
└─ README.md

```
## At a glance

- **Objective:** Medical image segmentation with clear, reproducible evaluation.
- **Scope:** End-to-end workflow — preprocessing → training → inference → analysis — contained in `med-seg.ipynb`.
- **Repo contents:**  
  - Notebook: `med-seg.ipynb`  
  - Visuals: `figures/` (all plots saved from the notebook)  
  - Placeholders: `reports/`, `data/`, `src/`
- **Preprocessing:** resizing/normalization; basic mask checks (as implemented in the notebook).
- **Evaluation artifacts:** pixel-level confusion matrix, ROC (AUC), Precision-Recall (AP), Dice/IoU (per-image + aggregate), Dice/IoU vs threshold, coverage-vs-Dice, histograms/box-plots, and best/worst/random qualitative panels.
- **Environment:** standard scientific Python (Jupyter + NumPy/Pandas + Matplotlib; add/adjust libraries to match your notebook).

  ## flowchart LR
    A[Inputs: images + masks] --> B[Preprocess\nresize • normalize • mask sanity checks]
    B --> C[Augment\nflip • rotate • blur/jitter (as used)]
    C --> D[Split\ndata → train / val / test]
    D --> E[Train model\n(e.g., U-Net family)\nloss: Dice/BCE/Combo • optimizer • LR schedule]
    E --> F[Inference\non val/test]
    F --> G[Probability maps\n(per-pixel)]
    G --> H[Threshold sweep\n0 → 1]
    H --> I[Post-processing\nsmall-obj removal • hole fill (optional)]
    I --> J[Metrics & Plots\nDice/IoU • Confusion • ROC/PR • Calibration • Panels]

