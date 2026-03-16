# Google Smartphone Decimeter Challenge 2022

Notebook workflow for the Kaggle **Smartphone Decimeter 2022** challenge: download raw GNSS/IMU data, build training features, analyze quality, and train baseline models that emit competition submissions.

## Data Layout

- Raw data lives under `train/` and `test/` (downloaded by `SC4000_INIT.ipynb` from Kaggle).
- Optional RTKLIB support uses `rtklib.netrc` for remote data fetches.
- Model outputs land in `SUBMISSIONS/` (one folder per model notebook).

## Environment

- Python 3.9+
- Jupyter Notebook or JupyterLab
- Kaggle account with API key (needed by `SC4000_INIT.ipynb`)

Install packages covering all notebooks:

```bash
pip install jupyter kaggle python-dotenv pandas numpy matplotlib seaborn pyproj requests pymap3d scipy scikit-learn lightgbm pykalman tqdm
```

Set Kaggle credentials before running anything that hits the API:

```bash
export KAGGLE_USERNAME="<your_kaggle_username>"
export KAGGLE_KEY="<your_kaggle_api_key>"
```

## Notebook Dependency Map

- `SC4000_INIT.ipynb` → downloads Kaggle competition data to `train/` and `test/`; required by all downstream notebooks.
- `SC4000_GROUNDTRUTH.ipynb` → reads `train/*/ground_truth.csv`; prepares consolidated ground-truth targets for training.
- `SC4000_IMU.ipynb` → reads `train/*/device_imu.csv`; outputs cleaned IMU tables (`device_imu.csv`).
- `SC4000_GNSS.ipynb` → reads `train/*/device_gnss.csv`; outputs cleaned GNSS tables (`device_gnss.csv`).
- `SC4000_DATA_WRANGLING.ipynb` → consumes ground-truth, IMU, and GNSS tables; merges and engineers model-ready features.
- `SC4000_EDA.ipynb` → consumes wrangled features for exploratory checks.
- `SC4000_TEST.ipynb` → consumes IMU/GNSS feature logic to build test-set features (`device_imu.csv`, `device_gnss.csv`).
- Modeling notebooks consume wrangled/train-test data and write submissions:
  - `SC4000_LINEAR_REGRESSION.ipynb` → `SUBMISSIONS/LINEAR_REGRESSION/submission.csv`
  - `SC4000_LIGHTGBM.ipynb` → `SUBMISSIONS/LIGHT_GBM/submission.csv`
  - `SC4000_RANDOM_FOREST.ipynb` → `SUBMISSIONS/RANDOM_FOREST/submission.csv`
  - `SC4000_LRLGBM_STACK.ipynb` → `SUBMISSIONS/DUMP/submission.csv`

## Recommended Run Order

1. `SC4000_INIT.ipynb`
2. `SC4000_GROUNDTRUTH.ipynb`
3. `SC4000_IMU.ipynb`
4. `SC4000_GNSS.ipynb`
5. `SC4000_DATA_WRANGLING.ipynb`
6. `SC4000_EDA.ipynb`
7. `SC4000_TEST.ipynb`
8. Any model notebook(s): Linear Regression / LightGBM / Random Forest / LRLGBM Stack

## Repro Tips

- Run notebooks from clean kernels to avoid stale state; rerun upstream notebooks if a dependency file is missing.
- Keep package versions aligned across machines to reduce numerical drift.
- Do not commit `.env`, Kaggle keys, or downloaded data; they are local-only.
