# CellDEx-HCC

**CellDEx-HCC** is a research-stage machine learning pipeline for hepatocellular carcinoma imaging analysis. The first phase focuses on building a reproducible public-data benchmark for liver and tumor segmentation using medical imaging datasets.

This project is currently in its early development stage and is not intended for clinical diagnosis or treatment decisions.

## Project Goal

The goal of CellDEx-HCC is to build a step-by-step AI research pipeline for HCC analysis, starting with public imaging datasets and later expanding toward clinical variables, biomarkers, and multimodal risk modeling.

The current focus is:

* loading public liver/HCC imaging datasets
* preprocessing CT/MRI medical images
* working with liver and tumor segmentation masks
* training baseline segmentation models
* evaluating model performance using standard medical imaging metrics
* visualizing model predictions against ground-truth masks

## Phase 1: Public Imaging Baseline

Phase 1 focuses on creating a working segmentation pipeline.

The first milestone is:

```text
Load scan
↓
Load ground-truth mask
↓
Display image-mask overlay
↓
Train baseline segmentation model
↓
Evaluate using Dice / IoU
↓
Document results
```

This phase is designed to establish a clean technical foundation before expanding into classification, biomarkers, or clinical decision-support models.

## Planned Datasets

Potential public datasets for Phase 1 include:

* LiverHccSeg
* HCC-TACE-Seg
* TCGA-LIHC imaging resources
* Other public liver tumor CT/MRI datasets

The project will begin with one dataset before expanding to additional datasets for external validation.

## Current Progress

* [x] Repository initialized
* [x] Project renamed to CellDEx-HCC
* [x] Update project structure for HCC imaging
* [ ] Add dataset exploration notebook
* [ ] Load first public HCC imaging scan
* [ ] Load corresponding segmentation mask
* [ ] Generate first image-mask overlay
* [ ] Build preprocessing pipeline
* [ ] Train baseline segmentation model
* [ ] Evaluate model performance
* [ ] Document Phase 1 results

## Tech Stack

* Python
* NumPy
* Pandas
* PyTorch
* MONAI
* scikit-image
* SimpleITK / NiBabel
* Matplotlib
* Jupyter Notebooks

## Repository Structure

```text
CellDEx-HCC/
│
├── README.md
├── requirements.txt
├── environment.yml
├── .gitignore
├── LICENSE
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── README.md
│
├── notebooks/
│   ├── 01_explore_dataset.ipynb
│   ├── 02_preprocess_images.ipynb
│   └── 03_baseline_training.ipynb
│
├── src/
│   ├── config.py
│   ├── dataset.py
│   ├── preprocess.py
│   ├── train.py
│   ├── evaluate.py
│   └── visualize.py
│
├── outputs/
│   ├── figures/
│   ├── predictions/
│   └── metrics/
│
└── docs/
    ├── phase1_plan.md
    ├── dataset_notes.md
    └── meeting_notes.md
```

## Important Note

CellDEx-HCC is a research project. It does not provide medical advice, diagnosis, prognosis, or treatment recommendations. Any future clinical use would require proper validation, ethics approval, privacy review, and regulatory consideration.
