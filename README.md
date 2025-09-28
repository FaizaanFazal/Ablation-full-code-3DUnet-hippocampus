# SegmentationUnet3D

Please cite our paper if you use this code or results: ( wil update soon after acceptance)
- Paper: [Title], [Journal], [Year], DOI: [add DOI]
- BibTeX (placeholder):
  @article{YourPaper2025, title={...}, author={...}, journal={...}, year={2025}, doi={...}}

## Project structure
- analysis.ipynb — analysis/evaluation used for reported MSD NP/FP scores and paired t-test.
- main.ipynb — training on HarP/ADNI (source domain).
- MSD_main.ipynb — transfer/evaluation on MSD.
- VNet.ipynb — backbone sanity check (VNet).
- segmentation/ — model classes (UNet3D, VNet) and helpers.
- NewHistory/ — training histories of models presented in the paper (reported).
- history/ — histories of previously trained models not presented (not reported).
- saved_plots/, qualitative_results/ — figures used in the paper.
- hippo_split.csv — MSD split used.

Notes on histories:
- NewHistory = presented (reported in the journal).
- history = not presented (not reported).

## Models
- UNet3D (primary model used in the paper). A diagram can be added if allowed (e.g., docs/unet_diagram.png).
- VNet (backbone check/baseline).

Trained models are large and not uploaded. Where size permits, small VNet weights may be included; UNet weights should be trained locally or downloaded from an external release if provided.

## Datasets and references
- ADNI (Alzheimer’s Disease Neuroimaging Initiative)
  - https://adni.loni.usc.edu/
  - Access requires registration and agreement to ADNI data use terms. Please cite ADNI per their guidance.
- Medical Segmentation Decathlon (MSD)
  - http://medicaldecathlon.com/
  - Use Task04_Hippocampus for these experiments.

## Environment
- Python 3.9.13
- Windows (example commands):
  - py -m venv .venv
  - .venv\Scripts\activate
  - py -m pip install -r requirements.txt

Conda alternative:
- conda create -n seg3d python=3.9.13
- conda activate seg3d
- pip install -r requirements.txt

## Data preparation
Raw and preprocessed pipelines (e.g., 3D CLAHE, SCE-3DWT) are provided in the notebooks. Update the path variables in the first cells to point to your dataset folders. Typical layout (adjust to your drive):
- ADNI/HarP raw: D:\data\ADNI\Task520_HarP\imageTr, labelTr
- HarP FP preprocessed: D:\data\ADNI\Task520_Harp_Preprocessed
- MSD: D:\data\MSD\Task04_Hippocampus\Processed\imagesTr, labelsTr

## How to run (recommended order)
1) main.ipynb — train on HarP (source domain).
2) MSD_main.ipynb — transfer/evaluate on MSD.
3) analysis.ipynb — compute NP/FP MSD scores (mean±std) and run the paired t-test.
4) VNet.ipynb — optional backbone check.

## analysis.ipynb: set your dataset paths
In analysis.ipynb, update the model_info dictionary to your local folders before running:
```python
model_info = {
    "HARP_NP": {
        "pth": "NewModels/UNet3D_NP_HARP_UPDATED.pth",
        "img_dir": r"<path-to-ADNI>\Task520_HarP\imageTr",
        "lbl_dir": r"<path-to-ADNI>\Task520_HarP\labelTr"
    },
    "HARP_FP": {
        "pth": "NewModels/UNet3D_FP_UPDATED.pth",
        "img_dir": r"<path-to-ADNI>\Task520_Harp_Preprocessed",
        "lbl_dir": r"<path-to-ADNI>\Task520_HarP\labelTr"
    },
    "HARP_CLAHE": {
        "pth": "NewModels/UNet3D_3D_CLAHE_UPDATED.pth",
        "img_dir": r"<path-to-repo>\3DCLAHE_PREPROCESSED",
        "lbl_dir": r"<path-to-ADNI>\Task520_HarP\labelTr"
    },
    "MSD_NP": {
        "pth": "NewModels/MSD_NP_BINARY_UPDATED.pth",
        "img_dir": r"<path-to-MSD>\Task04_Hippocampus\Processed\imagesTr",
        "lbl_dir": r"<path-to-MSD>\Task04_Hippocampus\Processed\labelsTr"
    },
    "MSD_FP": {
        "pth": "NewModels/MSD_FP_BINARY.pth",
        "img_dir": r"<path-to-MSD>\Task04_Hippocampus\Processed\Preprocessed\FP_PREPROCESSED",
        "lbl_dir": r"<path-to-MSD>\Task04_Hippocampus\Processed\labelsTr"
    },
    "MSD_FP_HARP":{ 
        "pth": "NewModels/Transfer_MSD_FP_to_HARP_FP.pth",
        "img_dir": r"<path-to-ADNI>\Task520_Harp_Preprocessed",
        "lbl_dir": r"<path-to-ADNI>\Task520_HarP\labelTr"
    },
    "MSD_NP_HARP":{ 
        "pth": "NewModels/Transfer_MSD_NP_to_HARP_NP.pth",
        "img_dir": r"<path-to-ADNI>\Task520_HarP\imageTr",
        "lbl_dir": r"<path-to-ADNI>\Task520_HarP\labelTr"
    }
}
```

## Reproducibility notes
- NewHistory/ contains the training logs/histories corresponding to models reported in the paper.
- history/ contains logs from exploratory or non-presented runs (not used in the paper).
- Evaluation in analysis.ipynb reproduces the reported NP/FP MSD scores and the paired t-test.
- Due to size limits, trained model weights are not committed. If external download links are provided (e.g., GitHub Releases/Zenodo), they will be listed here; otherwise, please train via the notebooks.

## Acknowledgments
- ADNI: https://adni.loni.usc.edu/
- MSD: http://medicaldecathlon.com/