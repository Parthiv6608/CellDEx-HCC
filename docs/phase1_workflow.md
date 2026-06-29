# Phase 1 Technical Workflow

CellDEx-HCC Phase 1 builds a reproducible baseline from public, de-identified liver/HCC imaging data. It is a research prototype only and must not be used for clinical diagnosis or treatment decisions.

## Workflow overview

```text
Public dataset
    -> load CT/MRI volume
    -> load segmentation mask
    -> visualize image and mask
    -> preprocess consistently
    -> make patient-level splits
    -> train baseline segmentation/classification model
    -> evaluate and document limitations
```

## 1. Select and document a public dataset

- Use only public, de-identified CT or MRI datasets whose license permits the planned research.
- Record the dataset name, source URL, version or access date, license, modality, annotation type, and cohort limitations.
- Store downloaded files under `data/raw/` or approved secure storage. Never commit medical images, patient data, or dataset archives.
- Assign internal subject identifiers if needed; do not infer or retain identifying information.

## 2. Load the CT/MRI volume

- Read DICOM series with `pydicom` or SimpleITK and NIfTI volumes with nibabel or SimpleITK.
- Preserve spatial metadata: voxel spacing, orientation, origin, affine matrix, and series identifiers.
- Validate the array shape, modality, intensity range, slice order, and expected anatomical coverage.
- Keep reusable loading and validation code in `src/data/`; use notebooks only for exploration.

## 3. Load and align the segmentation mask

- Load the provided liver or tumor mask and identify its label definitions.
- Verify that image and mask have matching dimensions and spatial coordinates.
- Display alignment checks before resampling. If resampling is necessary, use linear interpolation for images and nearest-neighbor interpolation for label masks.
- Treat missing, malformed, or ambiguous annotations as data-quality issues rather than silently correcting them.

## 4. Visualize image-mask pairs

- Show representative axial, coronal, and sagittal slices.
- Overlay the mask with transparency and include separate image-only and mask-only views.
- Check empty masks, disconnected labels, boundary alignment, orientation, and implausible voxel values.
- Save only non-identifying derived figures under `outputs/`; generated outputs remain local and are not committed.

## 5. Preprocess reproducibly

- Define modality-appropriate intensity handling, such as CT windowing/clipping or MRI normalization.
- Reorient volumes to a consistent convention and resample to a documented voxel spacing when required.
- Crop or pad to a consistent region and size without discarding annotated lesions.
- Apply deterministic transforms for validation/test data and record all training augmentation settings.
- Fit any data-dependent preprocessing using the training split only to avoid leakage.

## 6. Create patient-level splits

- Split train, validation, and test sets by patient, never by slice, series, or patch.
- Keep every scan from one patient in exactly one split.
- Use a fixed random seed and save a non-identifying split manifest or generation configuration.
- Report class and lesion distributions across splits; use grouped or stratified methods where the dataset supports them.

## 7. Train baseline models

### Segmentation baseline

- Start with a simple MONAI/PyTorch model such as 2D or 3D U-Net.
- Train on image-mask pairs with a documented loss, optimizer, learning rate, stopping rule, and random seed.
- Track Dice and IoU, plus per-case results and failure cases. Do not rely on an aggregate score alone.

### Classification baseline

- Define the prediction target and label provenance before training.
- Use patient-level labels and splits. If inputs are derived from segmentation, generate them without using held-out labels or test-set information.
- Begin with a transparent baseline and report sensitivity, specificity, ROC-AUC, and confidence intervals when sample size permits.

Model checkpoints belong in a local ignored directory such as `checkpoints/`; do not commit them.

## 8. Evaluate and document

- Evaluate once on the held-out test set after model and preprocessing decisions are fixed.
- Record dataset version, split, configuration, software environment, metrics, and qualitative examples.
- Describe dataset bias, annotation uncertainty, small-cohort limitations, domain shift, and failure modes.
- Frame all results as research findings from public/de-identified data, not as clinical performance or diagnostic claims.

## Initial completion criteria

Phase 1's first end-to-end milestone is complete when one public dataset can be loaded, one volume-mask pair can be visually verified, preprocessing can be reproduced from configuration, a patient-level split can be regenerated, and at least one baseline can be trained and evaluated without committing data, checkpoints, logs, or generated outputs.
