<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/finki-logo-dark.png">
    <img src="assets/finki-logo-light.png" alt="Faculty of Computer Science and Engineering, Ss. Cyril and Methodius University in Skopje" width="600">
  </picture>
</p>

# Graduation Thesis: Classic ML vs. LLMs for Colorectal Cancer Detection from Gut Microbiome Data

Can a large language model beat classic machine learning at detecting colorectal cancer (CRC) from gut bacteria profiles? The thesis first rebuilds the random forest classifier from a meta-analysis of 27 studies ([Pekel, Karcher et al., 2026](https://doi.org/10.1016/j.chom.2026.05.030)) in Python, following the paper's Methods. It then compares tuned classic models and LLMs against that baseline, with the same study-blocked evaluation.

## Phases

| Phase | Goal | Status |
|---|---|---|
| 1 | Rebuild the paper's data preparation from the published profiles | Done |
| 2A | Replicate the paper's random forest | Done |
| 2B | Tune the random forest and compare other classic models | Planned |
| 3 | Compare with an LLM: zero-shot, few-shot and LoRA fine-tuning | Planned |

## Repository layout

```
graduation_thesis/
├── assets/
│   ├── finki-logo-dark.png
│   └── finki-logo-light.png
├── data/
│   ├── processed/
│   │   └── phase_1/
│   │       ├── 02_balanced_subset/
│   │       │   └── balanced_samples.csv
│   │       └── 03_preprocessing/
│   │           ├── labels.csv
│   │           └── relab_347.csv
│   └── raw/
│       └── zenodo/
│           ├── Metadata.all.samples.tsv
│           └── Relab.all.samples.tsv
├── notebooks/
│   ├── phase_1/
│   │   ├── 01_data_overview.ipynb
│   │   ├── 02_balanced_subset.ipynb
│   │   └── 03_preprocessing.ipynb
│   └── phase_2/
│       └── phase_2a/
│           ├── 01_unified_random_forest.ipynb
│           └── 02_loso_random_forest.ipynb
├── results/
│   ├── figures/
│   │   ├── phase_1/
│   │   │   ├── 01_data_overview/
│   │   │   │   ├── genus_prevalence.png
│   │   │   │   └── samples_per_study.png
│   │   │   ├── 02_balanced_subset/
│   │   │   │   └── balance_per_study.png
│   │   │   └── 03_preprocessing/
│   │   │       └── normalization_example.png
│   │   └── phase_2/
│   │       └── phase_2a/
│   │           ├── 01_unified_random_forest/
│   │           │   ├── fold_sizes.png
│   │           │   └── roc_unified.png
│   │           └── 02_loso_random_forest/
│   │               ├── loso_per_study.png
│   │               ├── loso_vs_paper.png
│   │               └── scv_vs_paper.png
│   └── tables/
│       ├── phase_1/
│       │   └── 03_preprocessing/
│       │       └── genus_filter_rules.csv
│       └── phase_2/
│           └── phase_2a/
│               ├── 01_unified_random_forest/
│               │   └── unified_auc.csv
│               └── 02_loso_random_forest/
│                   ├── loso_auc.csv
│                   └── scv_auc.csv
├── .gitattributes
├── .gitignore
├── README.md
└── requirements.txt
```

## Setup

Requires Python 3.14.

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows
source .venv/bin/activate       # macOS / Linux
pip install -r requirements.txt
python -m ipykernel install --user --name graduation-thesis --display-name "Python (graduation-thesis)"
jupyter lab
```

The notebooks run on the `graduation-thesis` kernel registered above.

## Data

Harmonized genus-level profiles published with the paper on Zenodo, [record 20310630](https://zenodo.org/records/20310630) (CC BY 4.0). Both files are included in `data/raw/zenodo/`, and the first notebook checks their MD5 checksums.

| File | MD5 |
|---|---|
| `Relab.all.samples.tsv` | `cca9b0b616c721c5655ec1ba8825e260` |
| `Metadata.all.samples.tsv` | `e87644359858f853da198bce3e21b7de` |

## Citation

Pekel, S., Karcher, N., et al. (2026). Meta-analysis reveals microbiome signatures for colorectal cancer that are universal across age groups and sequencing methods. *Cell Host & Microbe*, 34, 1462–1476. https://doi.org/10.1016/j.chom.2026.05.030
