# 🌱 Pasture Biomass Prediction from Field Images

## Overview

Accurately estimating pasture biomass is a fundamental challenge in livestock and land management. Farmers rely on these estimates to decide when animals should graze, when paddocks need recovery, and how to maintain long-term pasture productivity. Small errors can lead to overgrazing, wasted feed, or reduced animal welfare.

This project focuses on predicting pasture biomass directly from **field images and ground-based measurements** using machine learning. The goal is to estimate multiple biomass components that are critical for grazing decisions, enabling faster, scalable, and more consistent assessment compared to traditional manual methods.

The work is based on the **CSIRO Biomass dataset**, which contains professionally annotated pasture images collected across different regions, seasons, and species compositions in Australia.

---

## Problem Definition

Given an image of a pasture along with associated metadata, the task is to predict five biomass components (in grams):

- Dry green vegetation (excluding clover)
- Dry dead plant material
- Dry clover biomass
- Green dry matter (GDM)
- Total dry biomass

Each prediction corresponds to a specific biomass component for a given pasture image.

---

## Dataset Description

The dataset combines **image data** with **tabular environmental and vegetation features**.

### Data Sources
- High-resolution pasture images
- Ground-truth biomass measurements
- Vegetation indices (NDVI)
- Canopy height measurements
- Location and species information

### Key Files
- `train.csv` — metadata and ground-truth biomass values
- `test.csv` — metadata for prediction
- `sample_submission.csv` — submission format
- `train_images/` — training images
- `test_images/` — test images

---

## Feature Overview

Each training record includes:

| Feature | Description |
|-------|------------|
| `image_path` | Path to the pasture image |
| `Sampling_Date` | Date of data collection |
| `State` | Geographic region |
| `Species` | Dominant pasture species |
| `Pre_GSHH_NDVI` | Normalized Difference Vegetation Index |
| `Height_Ave_cm` | Average canopy height |
| `target_name` | Biomass component being predicted |
| `target` | Biomass value (grams) |

Multiple records may correspond to the same image, each representing a different biomass component.

---

# Data Quality Report 

- A folder named Data Quality Report is made for DATA EXPLORATION.
- It has been categorized into two parts 1. Continuous Features 2. Categorical Features.
- Diagrams and graphs are included in each .

- Continuous Features
| Feature       |   Count |   % Miss. |   Card. |   Min |   1st Qrt. |    Mean |   Median |   3rd Qrt. |    Max |   Std. Dev. |
|:--------------|--------:|----------:|--------:|------:|-----------:|--------:|---------:|-----------:|-------:|------------:|
| Pre_GSHH_NDVI |    1785 |         0 |      65 |  0.16 |     0.56   |  0.6574 |     0.69 |     0.77   |   0.91 |      0.152  |
| Height_Ave_cm |    1785 |         0 |      81 |  1    |     3      |  7.596  |     4    |     7      |  70    |     10.2737 |
| target        |    1785 |         0 |    1328 |  0    |     4.8182 | 24.7823 |    18.2  |    35.9406 | 185.7  |     25.8237 |

## Data Characteristics

Exploration of the dataset reveals several important properties:

- Biomass values are **continuous and highly skewed**
- Different biomass components exist on **very different numerical scales**
- Some components (such as clover biomass) contain many near-zero values
- Several biomass targets are **strongly correlated**, reflecting shared biological structure
- Both image content and tabular measurements carry meaningful signal

These characteristics strongly influence model design and evaluation strategies.

---

## Modeling Perspective

This problem is treated as a **regression task with multiple related targets**.  
Effective solutions must:

- Handle skewed target distributions
- Capture relationships between biomass components
- Combine visual features from images with numeric and categorical metadata
- Avoid data leakage caused by repeated use of the same image across targets

The project emphasizes robustness, interpretability, and scalability rather than black-box prediction alone.

---

## Applications and Impact

Accurate pasture biomass estimation enables:

- Smarter grazing and stocking decisions
- Improved pasture recovery and sustainability
- Reduced reliance on manual sampling
- Better monitoring of pasture health over time

By integrating machine learning with real-world agricultural data, this project aims to support more sustainable and data-driven livestock systems.

---

## Acknowledgements

- CSIRO for providing the dataset and problem formulation
- Kaggle for hosting the competition and infrastructure
