# Earth-Observation

# Land Cover Classification using Satellite Imagery (Delhi-NCR)

This repository contains a complete pipeline for classifying land cover types over the Delhi-NCR region using high-resolution RGB satellite images and deep learning.

---

## Overview

We use spatial and raster data to:

* Filter relevant image tiles based on geographic bounds
* Extract land cover labels from ESA WorldCover 2021 data
* Train a ResNet18 model on RGB tiles
* Evaluate model performance using F1 scores, confusion matrix, and visual samples

---

## Project Objectives

* Learn to preprocess geospatial vector and raster data
* Build a supervised image classification dataset from scratch
* Train a CNN model to classify satellite images
* Visualize prediction performance and confusion

---

## Folder Structure

```
EarthObs/
├── delhi_ncr_region.geojson         # Vector boundary of Delhi-NCR
├── delhi_airshed.geojson            # Larger airshed region (optional)
├── worldcover_bbox_delhi_ncr_2021.tif  # ESA WorldCover raster
├── rgb/                             # 128x128 image tiles (named by lat_lon)
└── train_eval.ipynb                 # Full Colab-compatible training pipeline
```

---

## Data Sources

* Planet
* RGB image patches with geospatial naming (e.g. `28.5355_77.3910.png`)
* Regional boundaries (GeoJSON)

---

## How It Works

1. **Geo-filtering**: Read and project NCR shapefile, overlay a 60x60 km grid
2. **Image selection**: Parse lat/lon from filenames and select images within bounds
3. **Label extraction**: Use rasterio to crop 128x128 patches from `.tif` raster
4. **Labeling**: Assign ESA class code based on dominant class in the patch
5. **Training**: Train ResNet18 on the RGB image-label pairs
6. **Evaluation**: Report accuracy, macro F1, confusion matrix, and prediction samples

---

## Model

* **Architecture**: ResNet18 (pretrained)
* **Input**: 128x128 RGB images
* **Output**: 8-class classification based on ESA land cover
* **Tools**: PyTorch, torchvision, torchmetrics, matplotlib, seaborn

---

## Quick Start (Colab)

```python
# Mount Drive
from google.colab import drive
drive.mount('/content/drive')

# Follow steps in train_eval.ipynb
```

---

## Sample Results

* Train Accuracy: 92.9%
* Test Accuracy: 64.0%
* Macro F1 Score: \~0.22
* Strongest performance on Cropland and Built-up
* Most confusion occurs on minority classes

---

## To Improve

* Use multispectral or NDVI bands
* Augment underrepresented classes
* Explore temporal or higher resolution datasets

---

## Contributors

* Built by: \[Your Name / Team Name]
* License: MIT

---

## Acknowledgements

* ESA WorldCover 2021
* PyTorch & torchvision
* GeoPandas, Rasterio, Seaborn
