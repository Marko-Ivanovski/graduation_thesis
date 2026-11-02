<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/finki-logo-dark.png">
    <img src="assets/finki-logo-light.png" alt="Faculty of Computer Science and Engineering, Ss. Cyril and Methodius University in Skopje" width="600">
  </picture>
</p>

# Graduation Thesis: Classic ML vs. LLMs for Colorectal Cancer Detection from Gut Microbiome Data

Can a large language model beat classic machine learning at detecting colorectal cancer (CRC) from gut bacteria profiles? This thesis first replicates the random forest classifier from a recent meta-analysis of 27 studies and 5,966 samples ([Pekel, Karcher et al., 2026](https://doi.org/10.1016/j.chom.2026.05.030)) in Python. It then compares tuned classic models and fine-tuned LLMs against that baseline, using the same study-blocked evaluation.

## Phases

| Phase | Goal | Status |
|---|---|---|
| 1 | Rebuild the paper's data preparation from the published profiles | In progress |
| 2A | Replicate the paper's random forest and match its AUCs | Planned |
| 2B | Tune the random forest and compare other classic models | Planned |
| 3 | Compare with an LLM: zero-shot, few-shot and LoRA fine-tuning | Planned |

## Repository layout

```
assets/          images used by this README
data/raw/zenodo/ input tables from Zenodo (see Data)
data/processed/  CSV files produced by the notebooks, one folder per notebook
notebooks/       one folder per phase, notebooks numbered in run order
results/         figures/ and tables/, each with one folder per notebook
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

The notebooks use the `graduation-thesis` kernel, which the `ipykernel` line registers once and which always runs this environment's Python. To run a notebook from the command line, use `python -m nbconvert --to notebook --execute --inplace <notebook>` from the activated environment. Run the notebooks in order, phase by phase.

## Data

The notebooks start from the harmonized genus-level profiles published with the paper on Zenodo, [record 20310630](https://zenodo.org/records/20310630) (CC BY 4.0). The two files are included in `data/raw/zenodo/`:

| File | MD5 |
|---|---|
| `Relab.all.samples.tsv` | `cca9b0b616c721c5655ec1ba8825e260` |
| `Metadata.all.samples.tsv` | `e87644359858f853da198bce3e21b7de` |

The first notebook checks both checksums before doing anything else.

## Results

In progress.

## Citation

Pekel, S., Karcher, N., et al. (2026). Meta-analysis reveals microbiome signatures for colorectal cancer that are universal across age groups and sequencing methods. *Cell Host & Microbe*, 34, 1462–1476. https://doi.org/10.1016/j.chom.2026.05.030
