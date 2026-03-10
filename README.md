# Google Smartphone Decimeter Challenge 2022

Notebook-based pipeline for the Kaggle **Smartphone Decimeter 2022** challenge.

This project processes raw smartphone sensor data (GNSS + IMU), builds training features, performs exploratory analysis, and trains a baseline linear regression model.

## Repository Contents

- `SC4000_INIT.ipynb` - Environment setup and Kaggle dataset download.
- `SC4000_GROUNDTRUTH.ipynb` - Ground-truth target preparation.
- `SC4000_IMU.ipynb` - IMU data extraction and preparation.
- `SC4000_GNSS.ipynb` - GNSS data extraction and preparation.
- `SC4000_DATA_WRANGLING.ipynb` - Dataset merging, cleaning, and feature engineering.
- `SC4000_EDA.ipynb` - Exploratory data analysis and feature/target inspection.
- `SC4000_TEST.ipynb` - Test-set feature preparation.
- `SC4000_LINEAR_REGRESSION.ipynb` - Baseline model training and evaluation.
- `SUBMISSIONS/submission.csv` - Example submission output.

## Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab
- Kaggle account and API credentials

Install core packages:

```bash
pip install jupyter kaggle python-dotenv pandas numpy matplotlib seaborn scikit-learn pyproj requests
```

## Kaggle Authentication

Set credentials via environment variables before running notebooks that call the Kaggle API:

```bash
export KAGGLE_USERNAME="<your_kaggle_username>"
export KAGGLE_KEY="<your_kaggle_api_key>"
```

Recommended: store these in a local `.env` file (not committed to git).

## Run Order

Run notebooks in this order to satisfy dependencies:

1. `SC4000_INIT.ipynb`
2. `SC4000_GROUNDTRUTH.ipynb`
3. `SC4000_IMU.ipynb`
4. `SC4000_GNSS.ipynb`
5. `SC4000_DATA_WRANGLING.ipynb`
6. `SC4000_EDA.ipynb`
7. `SC4000_TEST.ipynb`
8. `SC4000_LINEAR_REGRESSION.ipynb`

## Pipeline Dependency Summary

- `GROUNDTRUTH`, `IMU`, and `GNSS` produce source datasets.
- `DATA_WRANGLING` merges and engineers model-ready features.
- `EDA` validates feature quality and relationships.
- `TEST` prepares inference-time features.
- `LINEAR_REGRESSION` consumes wrangled/train-test artifacts for baseline modeling.

## Quick Start

```bash
jupyter notebook
```

Open the notebooks and execute cells from top to bottom in the run order above.

## Reproducibility Notes

- Run each notebook from a clean kernel to avoid stale variables.
- If a notebook fails due to missing intermediate files, rerun upstream notebooks.
- Keep package versions consistent across machines to reduce numeric/output drift.

## Security Note

Do not hardcode Kaggle keys inside notebooks. Use environment variables or `.env` locally.
