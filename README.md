# Wavelet–Transformer–XGBoost with CBO for Irradiance Prediction

**Publication:** Hybrid Wavelet–Transformer–XGBoost Model Optimized by Chaotic Billiards for Global Irradiance Forecasting  
**Journal:** Journal of Sensor and Actuator Networks (2026)  
**DOI:** https://doi.org/10.3390/jsan15010012

## Method

A wavelet-oriented representation and Transformer-style temporal encoder produce a base forecast. XGBoost then models residual structure using a separate calibration slice. Hyperparameter search is exposed through the CBO-related experiment interface.

The project includes chronological data preparation, model fitting, optional hyperparameter selection, evaluation metrics and graphical diagnostics. The architecture family and training parameters are configured in [config.json](config.json).

## Input data

The training script accepts a time-ordered multivariate CSV with a numeric `target` column. The target in this study is **global irradiance**. Dataset columns and evaluation assumptions are discussed in [data/README.md](data/README.md). Source data must be obtained from the study's experimental dataset and should be kept distinct from the synthetic software check.

## Installation and execution

```bash
python -m venv .venv
pip install -r requirements.txt
pytest -q
python train.py --smoke --epochs 2 --out outputs/smoke
```

With measured time-series data:

```bash
python train.py --csv path/to/measurements.csv --target target --time-col time --epochs 40 --out outputs/experiment
```

The program saves training history, test predictions, error metrics, and a fitted checkpoint under the chosen output directory. Optional parameter search is supported through `--search paper --trials N`, subject to the method-specific qualifications below.

## Evaluation notes

The CBO implementation currently uses an illustrative chaotic search rather than a fully audited transcription of the published billiards optimizer. Results should be reported as independent experiments until that audit is complete.

The test interval is chronological. Normalization statistics must be estimated on training data, and all reported comparisons should specify the time span, forecast horizon, seed, target units and metric definitions. [REPRODUCIBILITY.md](REPRODUCIBILITY.md) records the implementation boundaries and outstanding experimental checks.
