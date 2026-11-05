# NSSP_lab1# NSSP Miniproject 1 – Language task fMRI (Group A)

NX-421 Neural Signals and Signal Processing, EPFL, Fall 2026.

We map brain activity during the Human Connectome Project (HCP) language task: one subject, one run (316 volumes, TR = 0.72 s), alternating story blocks (Aesop fables) and math blocks (spoken arithmetic).

- **Part 1:** preprocessing and a hypothesis-driven GLM (story vs math contrast, Yeo 7-network comparison).
- **Part 2 (variant 1):** data-driven PCA, with one timepoint as one sample, and correlation of the PCA scores with the GLM regressors.

## Structure

```
GROUPA_miniproject_1/
├── GROUPA_report.pdf          # Written report
├── GROUPA_presentation.mp4    # Video presentation
├── GROUPA_code.ipynb          # Full analysis, run top to bottom
├── utils.py                   # Helpers from the labs (FSL setup, FSLeyes viewer, mkdir)
├── dataset_description.md     # Short description of the dataset
├── atlases/
│   └── Yeo2011_7Networks_MNI152_FreeSurferConformed1mm_LiberalMask.nii.gz
└── raw_data/                  # Input data (NIfTI images not included, see below)
    ├── T1/T1w.nii.gz
    └── fMRI/tfMRI_LANGUAGE_LR/
        ├── tfMRI_LANGUAGE_LR.nii.gz
        └── tfMRI_LANGUAGE_LR_task_onsets.csv
```

Running the notebook also creates `derivatives/` (preprocessed images) and `figures/` (report figures).

## Notebook sections

0. **Data inspection:** image sizes, voxel size, TR, orientation.
1. **Structural preprocessing:** skull stripping (BET), segmentation (FAST), registration to MNI152 (FLIRT, then ANTs SyN).
2. **Functional preprocessing:** motion correction and framewise displacement (MCFLIRT), 6 mm Gaussian smoothing, anatomical–functional alignment check.
3. **GLM:** design matrix, regressor correlations, single-condition maps, story vs math contrast, overlap with the Yeo networks.
4. **PCA:** PCA on the smoothed run, scree plot and axial loading maps of the first 5 components, correlation of the first 10 scores with the GLM regressors.

## How to run

1. Run on Neurodesk with FSL 6.0.7.18, FreeSurfer 7.4.1 and ANTs 2.6.5. The first cell loads these modules.
2. Python packages: `nibabel`, `nilearn`, `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `fsleyes`.
3. Place the dataset images (`T1w.nii.gz`, `tfMRI_LANGUAGE_LR.nii.gz`) in `raw_data/` as shown above.
4. Run `GROUPA_code.ipynb` from top to bottom.