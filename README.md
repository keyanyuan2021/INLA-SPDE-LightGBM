Migration-Adjusted Lung Cancer Burden in China

Overview

This repository contains the R analysis code supporting a nationwide ecological modeling study of migration-adjusted lung cancer incidence and mortality in China. The analytical workflow integrates cancer registry data, Bayesian spatiotemporal modeling, and machine learning to estimate lung cancer burden at high spatial resolution.

The supplied analysis script includes implementations of MCMC-based Bayesian modeling, INLA-SPDE spatial/spatiotemporal modeling, LightGBM residual learning, time-ordered sliding-window, SHAP-based model interpretation, and prediction for 2,845 counties and future years through 2030. The original script also contains model diagnostics, mesh sensitivity analyses, feature-importance analyses, and uncertainty calculations.

Main analytical workflow

Data preprocessing — imports registry, population, geographic, and covariate data; standardizes selected variables and prepares model inputs.

Bayesian benchmark model — fits negative-binomial Bayesian hierarchical models using brms/MCMC and evaluates posterior diagnostics and predictive performance.

INLA-SPDE modeling — constructs spatial meshes and SPDE components, combines point and areal data, and estimates spatial, temporal, and covariate effects.

INLA-SPDE + LightGBM — uses LightGBM to model residual structure after the Bayesian spatiotemporal component and combines both components for final predictions.

Model validation — includes time-ordered sliding-window validation, with RMSE, MSE, ME, MAE, and R² as performance metrics.

Model interpretation — evaluates feature importance and SHAP values and generates summary/dependence plots.

Prediction — produces county-level estimates for 2020 and projections for 2021–2030, including uncertainty summaries.

Software and R packages

The analysis was developed in R. Major packages used in the supplied code include:

INLA, inlabru

brms

lightgbm

sf, sp, rgdal, raster

Matrix

dplyr, data.table, readxl, openxlsx

caret

ggplot2, patchwork

shapviz, fastshap

gstat

Some packages, particularly INLA and LightGBM, may require installation procedures beyond a standard install.packages() call.

Data availability

The repository provides analytical code but does not redistribute the underlying cancer registry, population, geographic, or covariate datasets. Users should obtain data from the sources described in the accompanying manuscript and prepare them with the variable names and structures expected by the scripts.

The original code contains local file paths used during analysis. Before running the code, replace these paths with paths appropriate to your computing environment. config/paths_template.R provides a suggested starting point for centralizing local paths.

Reproducibility notes

Set a reproducible random seed before stochastic model fitting or resampling. The supplied workflow uses set.seed(123) in several analyses.

The MCMC, INLA-SPDE, and LightGBM analyses can be computationally intensive; runtime and memory requirements depend on the input data and hardware.

Spatial analyses require compatible coordinate reference systems and valid geographic geometries.

Prediction datasets must contain the same covariates and compatible factor/index definitions as the model-fitting datasets.

Model objects and large derived outputs are not included in this repository.


Contact

Questions regarding the analytical workflow or additional reproducibility information may be directed to the corresponding author of the associated manuscript.
