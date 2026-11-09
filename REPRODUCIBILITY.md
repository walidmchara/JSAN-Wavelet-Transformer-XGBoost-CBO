# Experimental reproducibility

**Study:** Hybrid Wavelet–Transformer–XGBoost Model Optimized by Chaotic Billiards for Global Irradiance Forecasting  
**DOI:** https://doi.org/10.3390/jsan15010012

## Scope of implementation

The predictive structure combines a wavelet-oriented Transformer base model with XGBoost residual correction. A CBO-related hyperparameter search interface is included.

The CBO search is an illustrative chaotic optimization routine, not a validated reproduction of the published billiards optimizer. Residual correction must use separate calibration data and a fixed untouched test period.

## Data handling and evaluation

Measured data are supplied as an external time-ordered CSV rather than packaged with the source code. Normalization statistics and fuzzy-regime parameters, where used, must be fitted on training observations only. Input windows must not include future target values.

The default training workflow uses chronological partitions for model development, residual calibration (when applicable), validation and final evaluation. Multiple cities, sites, meteorological regimes or horizons need separately documented holdout protocols; a successful single-series run is not evidence of generalization.

## Reporting requirements

A repeatable experiment records the source dataset and its license, feature definitions, sampling period, target units, forecast horizon, random seeds, optimizer budget, train/test boundaries and all metric definitions. The software check `python train.py --smoke` uses simulated signals and serves only to validate execution.

Paper-level numerical agreement has not been independently established. The results of new runs should be reported as new experiments, with explicit comparison settings rather than attributed to the published results.
