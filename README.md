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

## 📂 Repository Overview & Structure

```bash
medical-image-segmentation-nitr-winter24/
├── data/                   # Dataset (Kvasir-SEG) or placeholder for download
├── reports/                # Generated reports, logs, evaluation metrics
├── src/                    # Training & model code (PyTorch Lightning modules, utils)
├── med-seg.ipynb           # Main Jupyter notebook (EDA, training, evaluation, plots)
├── LICENSE                 # MIT license
├── README.md               # Project documentation (this file)
```
## ⚙️ Setup & Usage

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/git-tarik/medical-image-segmentation-nitr-winter24.git
cd medical-image-segmentation-nitr-winter24
```

# create virtual environment
python -m venv venv
source venv/bin/activate   # (Linux/Mac)
venv\Scripts\activate      # (Windows)

# install dependencies
pip install -r requirements.txt
```
data/
└── Kvasir-SEG/
    ├── images/        # original images
    └── masks/         # corresponding segmentation masks
```

## 📊 Results & Visualizations

This project reports both **quantitative metrics** (Dice, IoU, ROC-AUC, PR-AUC, calibration) and **qualitative visualizations** (best/worst/random predictions).  

---

### 🔢 Quantitative Metrics

#### ✅ Confusion Matrix (Validation)
<p align="center">
  <img src="./reports/figure_03.png" width="400"/>
</p>
<p align="center"><em>Pixel-level confusion matrix on validation set — highlights dominant false positive/negative modes.</em></p>

#### 📈 ROC Curve (Validation)
<p align="center">
  <img src="./reports/figure_04.png" width="400"/>
</p>
<p align="center"><em>Receiver Operating Characteristic curve (pixel-level). AUC summarises separability across thresholds.</em></p>

#### 📊 Per-image Dice Histogram
<p align="center">
  <img src="./reports/figure_06.png" width="400"/>
</p>
<p align="center"><em>Distribution of per-image Dice scores — shows variance across images and highlights long-tail failures.</em></p>

---

### 🎨 Qualitative Results

#### 🔍 Quick EDA (Overlay Samples)
<p align="center">
  <img src="./reports/figures/quick_eda_overlays.png" width="500"/>
</p>
<p align="center"><em>Visual sanity-check: input images with ground-truth masks and predicted overlays.</em></p>

#### 🖼️ Result Gallery (Best / Worst / Random Predictions)
<p align="center">
  <img src="./reports/figures/result_gallery.png" width="600"/>
</p>
<p align="center"><em>Qualitative audit showing representative predictions.  
Panels are grouped into Top-6 best, worst, and random samples.  
Green = True Positive, Yellow = False Positive, Cyan = False Negative.</em></p>
