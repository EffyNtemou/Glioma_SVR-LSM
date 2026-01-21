# Voxelwise Statistics & Atlas-Based Overlap Analysis

This repository contains two Python scripts for voxelwise analyses of lesion masks
in a common brain space (e.g. MNI):

1. **Voxelwise total lesion volume statistics**
2. **Atlas-based voxel counting for overlapping lesion maps**

Both scripts operate on binary NIfTI lesion maps and produce outputs suitable for
visualization or statistical analysis.

---

## Script 1: Voxelwise Total Lesion Volume Statistics

### Purpose

This script computes **voxelwise statistics of patient-level total lesion volume**.

For each voxel **v**:
- All patients with a lesion at **v** are identified
- For each of those patients, the **total lesion volume** is computed
- The voxel is assigned:
  - the **mean**
  - the **standard deviation**
  of those total lesion volumes.

Only voxels lesioned in at least a minimum number of patients are included.

---

### Output

The script produces two NIfTI files:

- `lesion_totalvol_mean_given_voxel.nii`  
- `lesion_totalvol_std_given_voxel.nii`

---

### Interpretation

At a voxel **v**:

- **Mean map value**  
  = average total lesion volume among patients who have a lesion in **v**

- **Standard deviation map value**  
  = variability of total lesion volume among those patients

This allows identification of brain regions preferentially involved in patients
with larger or smaller overall lesion burden.

---

## Script 2: Atlas-Based Voxel Counting for Overlapping Lesion Maps

### Purpose

This script quantifies how many voxels from the **overlap of two binary maps**
fall within each region of a brain atlas (e.g. Brainnetome; Fan et al., 2016).

The workflow is:
1. Compute voxelwise overlap between two binary maps
2. Save the overlap as a new NIfTI file
3. Count overlapping voxels within each atlas region
4. Print voxel counts per region

---

### Output

- One NIfTI file:
  - `overlap_map.nii`
- Printed voxel counts for each atlas region

---

### Interpretation

For each atlas region:

> *How many voxels are shared between the two input maps within this region?*

This is useful for summarizing spatial overlap in anatomically defined regions.

---

## Requirements

- Python ≥ 3.8
- `numpy`
- `nibabel`
