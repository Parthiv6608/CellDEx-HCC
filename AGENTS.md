# CellDEx-HCC Agent Instructions

CellDEx-HCC is a research project for building a reproducible Python-based medical imaging machine learning pipeline for hepatocellular carcinoma (HCC) research.

## Current scope
Phase 1 focuses on public/de-identified liver/HCC imaging datasets only. The goal is not clinical deployment or diagnosis. The current goal is to:
- identify suitable public datasets
- load CT/MRI medical imaging files
- visualize scans and segmentation masks
- build baseline segmentation/classification workflows
- document limitations clearly

## Technical stack
Use Python, PyTorch, MONAI, nibabel, SimpleITK, pydicom, NumPy, pandas, matplotlib, scikit-learn, and Jupyter.

## Safety and data rules
- Do not commit datasets, DICOM files, NIfTI files, model checkpoints, or patient data.
- Keep all data inside local `data/` folders or secure storage.
- GitHub should contain code, configs, docs, and small synthetic/test files only.
- Do not make clinical diagnosis claims.
- Frame outputs as research prototypes only.

## Coding style
- Prefer simple, readable code.
- Build in small steps.
- Add comments for beginner readability.
- Keep notebooks for exploration and scripts for reusable workflows.
- Use patient-level splits when datasets contain multiple scans per patient.
