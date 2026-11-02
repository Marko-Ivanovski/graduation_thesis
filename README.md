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
├── assets/                                      logos for this README
│   ├── finki-logo-dark.png
│   └── finki-logo-light.png
├── data/
│   ├── raw/
│   │   └── zenodo/                              published input tables (Zenodo record 20310630)
│   │       ├── Metadata.all.samples.tsv         one row per sample: diagnosis, study, country, assay
│   │       └── Relab.all.samples.tsv            relative abundance of each genus in each sample
│   └── processed/                               files a notebook writes for later notebooks
│       └── phase_1/
│           ├── 02_balanced_subset/
│           │   └── balanced_samples.csv         the 5,966 balanced CRC and control samples
│           └── 03_preprocessing/
│               ├── labels.csv                   study, assay and label (1 = CRC) per sample
│               └── relab_347.csv                raw shares of the paper's 347 genera
├── notebooks/                                   run in this order
│   ├── phase_1/                                 data preparation
│   │   ├── 01_data_overview.ipynb               checksums, loading, the data as an ML problem
│   │   ├── 02_balanced_subset.ipynb             CRC vs control, balanced inside every study
│   │   └── 03_preprocessing.ipynb               the 347-genus filter and the normalization
│   └── phase_2/
│       └── phase_2a/                            random forest replication
│           ├── 01_unified_random_forest.ipynb   study-blocked 10×10 cross-validation
│           └── 02_loso_random_forest.ipynb      leave-one-study-out and within-study CV
├── results/
│   ├── figures/                                 PNG figures, one folder per notebook
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
│   └── tables/                                  CSV tables, one folder per notebook
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
├── .gitattributes                               keeps data files byte for byte (no line-ending changes)
├── .gitignore
├── README.md
└── requirements.txt                             pinned Python packages
```

Every folder under `data/processed/` and `results/` mirrors the notebook that writes it.

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
