# SegmentationUnet3D

This repository provides a comprehensive framework for 3D medical image segmentation, focusing on hippocampus segmentation from MRI volumes. It implements and benchmarks several 3D U-Net-based models with advanced features such as dropout, residual connections, and various preprocessing pipelines.

## Features

- **3D U-Net with Dropout and Residuals:** Robust PyTorch implementation for volumetric segmentation.
- **Flexible Preprocessing:** Supports raw, CLAHE-enhanced, and wavelet-transformed (SCE-WT) MRI data.
- **Extensive Metrics:** Computes Dice, Jaccard, F1, IoU, OSR, USR, ASD, Hausdorff, and more.
- **Training & Evaluation Scripts:** End-to-end pipelines for training, validation, and testing, including early stopping and learning rate scheduling.
- **Transfer Learning:** Utilities for fine-tuning models pretrained on the MSD dataset to the ADNI HarP dataset.
- **Visualization:** Tools for overlaying predictions, plotting training curves, and comparing preprocessing effects.
- **Reproducible Experiments:** Jupyter notebooks for ablation studies and result analysis.

## Data

- **ADNI HarP Dataset:** Hippocampus MRI volumes and labels.
- **MSD Hippocampus Dataset:** For transfer learning experiments.

## Usage

1. **Preprocessing:** Scripts for CLAHE and SCE-WT preprocessing of NIfTI volumes.
2. **Training:** Launch training via provided notebooks or scripts, specifying preprocessing type and model variant.
3. **Evaluation:** Evaluate trained models on test sets and visualize overlays.
4. **Transfer Learning:** Fine-tune MSD-trained models on HarP data with minimal code changes.

## Structure

- `main.ipynb` — Main notebook for experiments, ablations, and visualizations.
- `segmentation/model.py` — Model definitions (3D U-Net variants).
- `dataloaders.py` — Dataset and DataLoader utilities for NIfTI volumes.
- `SC3DWT.ipynb`, `MSD_main.ipynb` — Specialized notebooks for SCE-WT and MSD experiments.
- `3DCLAHE_PREPROCESSED/`, `NewModels/`, `NewHistory/` — Preprocessed data and model checkpoints.

## Final Trained Models

The following are the final trained models used in our experiments. All are located in the `/NewModels` directory. Please use these for evaluation and inference. The `/models` directory contains older models trained with different parameters and should not be used for final results.

```python
model_info = {
    "HARP_NP": {
        "pth": "NewModels/UNet3D_NP_HARP_UPDATED.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\imageTr",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\labelTr"
    },
    "HARP_FP": {
        "pth": "NewModels/UNet3D_FP_UPDATED.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_Harp_Preprocessed",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\labelTr"
    },
    "HARP_CLAHE": {
        "pth": "NewModels/UNet3D_3D_CLAHE_UPDATED.pth",
        "img_dir": r"D:\Faizaan\1_DATA_PROJECTS\Projects\SegmentationUnet3D\3DCLAHE_PREPROCESSED",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\labelTr"
    },
    "MSD_NP": {
        "pth": "NewModels/MSD_NP_BINARY_UPDATED.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\MSD Dataset\Task04_Hippocampus\Processed\imagesTr",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\MSD Dataset\Task04_Hippocampus\Processed\labelsTr"
    },
    "MSD_FP": {
        "pth": "NewModels/MSD_FP_BINARY.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\MSD Dataset\Task04_Hippocampus\Processed\Preprocessed\FP_PREPROCESSED",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\MSD Dataset\Task04_Hippocampus\Processed\labelsTr"
    },
    "MSD_FP_HARP":{ 
        "pth": "NewModels/Transfer_MSD_FP_to_HARP_FP.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_Harp_Preprocessed",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\labelTr"
    },
    "MSD_NP_HARP":{ 
        "pth": "NewModels/Transfer_MSD_NP_to_HARP_NP.pth",
        "img_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\imageTr",
        "lbl_dir": r"D:\Faizaan\AlzhimersData\ADNI\HippoCampus_labels_data\Task520_HarP\labelTr"
    }
}
```

- **Note:** All models above are in `/NewModels`. The `/models` folder contains legacy checkpoints not used for final results.

## Included Code and Analysis

- All model class code and computing functions are provided.
- `analysis.ipynb` contains statistical analysis (including Wilcoxon tests) and qualitative results.
- Results from previous/old tests are also included for reference.
- `hippo_split.csv` shows the train/validation/test split for the MSD dataset.

## Usage Instructions

1. **Create Environment:**  
   Use Python 3.9.13 and install dependencies from `requirements.txt`.
   ```bash
   conda create -n segunet3d python=3.9.13
   conda activate segunet3d
   pip install -r requirements.txt
   ```
2. **Prepare Data:**  
   Download ADNI and MSD datasets (open access) and preprocess as needed. Data cannot be redistributed due to licensing.
3. **Load Models and Data:**  
   Use the provided model checkpoints from `/NewModels` and point to the correct image/label directories as shown in `model_info`.
4. **Run Analysis:**  
   Use the provided notebooks/scripts for evaluation, visualization, and statistical analysis.
5. **Reproduce Results:**  
   All code for training, evaluation, and ablation is included. See `main.ipynb` and other notebooks for workflows.

## Requirements

- Python 3.8+
- PyTorch, NumPy, nibabel, scikit-image, matplotlib, seaborn, scikit-learn

## Citation

If you use this codebase, please cite the repository or related publications ( will be added soon).

---
