# What Makes a Good Negative?

Team 16 (CSE 494/559)

## Environment setup

Use Python 3.11 and Git. The predictor commands below are for Apple Silicon Macs
and also need Conda and Rosetta. Run the setup once from this folder:

```bash
python3.11 -m venv .venv
.venv/bin/python -m pip install -r requirements_combined.txt
.venv/bin/python -m ipykernel install --sys-prefix --name cse559-final --display-name "Python (CSE 559 project)"

cd tcr_predictors/epitcr
git clone https://github.com/ddiem-ri-4D/epiTCR.git
bash setup_mac.sh
epitcr_env/bin/python check_env.py

cd ../titan
git clone https://github.com/PaccMann/TITAN.git
bash setup_mac.sh
conda run -n titan python check_env.py

cd ../..
```

The combined file installs the preprocessing, evaluation, hard-negative, and notebook packages.
The predictor setup follows its [guide](tcr_predictors/GUIDE.md). The notebook runs prediction and scoring.

## How to run

```bash
.venv/bin/jupyter lab final.ipynb
```

Select **Python (CSE 559 project)**. `N_JOBS` sets how many folds run at once.
Project guides:

- Farhan: [preprocessing](preprocessing/GUIDE.md).
- Argha: [evaluation and controls](evaluation/GUIDE.md).
- Jacob: [two published predictors](tcr_predictors/GUIDE.md).
- Aditi: [hard negatives and robustness](hard_negatives/GUIDE.md).

Keep these three raw inputs in `data/`: `iedb_positives.csv`, `vdjdb_positives.csv`, and
`tcr_all_contig_annotations.csv`. They are already included; the code does not download them.
Preprocessing creates `folds.tsv` if missing, then reuses it. Keep the saved split for comparisons.
Data-source links are at the beginning of the notebook. The run saves `results/RESULTS.md`,
plots in `results/figures/`, and detailed files in `results/supporting/`.
The notebook downloads the receptor/reference sequences, prepares the folding inputs, and runs both
released predictors on the shared benchmark. ESM-2 downloads on first use. Boltz uses a CUDA GPU
when available, otherwise CPU; the complete folding audit takes substantial time on CPU.

## Interim results

`interim.ipynb` was run locally to check the integration and get preliminary results.
See [RESULTS.md](interim_results/RESULTS.md).
