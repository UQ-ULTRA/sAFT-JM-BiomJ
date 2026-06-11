# Bayesian joint modelling using semiparametric accelerated failure time approaches

## Model fitting example and guide

This repository contains code to generate data and fit the models proposed and discussed within the *Biometrical Journal* submission paper titled **“Bayesian joint modelling using semiparametric accelerated failure time approaches”**.

The goal of this paper pertained to the development of the novel **sAFT-JM** (*semiparametric accelerated failure time joint model*) framework with the use of **Bernstein Polynomials (BPs)** for flexible baseline hazard specification, with simulation studies demonstrating parameter recovery in a joint modelling context across an array of data generation scenarios.

In this file, we show the key programs used as components for our simulation study in a minimal form, for the purpose of comprehensibility.

---

## Repository files

### `datagen.R`

The file containing functions relevant for data generation. The key function, `simulate_joint_dataset`, generates joint longitudinal and survival datasets with individual-level random effects.

This real-world-inspired data generation scheme assigns participants to an equal size of each treatment, with options for users to choose between:

* log-logistic or Weibull true baseline hazards,
* censoring proportions: administrative, none, or 50% censoring,
* treatment effects.

---

### `saft_jm_fit.R`

Primary file for fitting the proposed sAFT joint model.

This first loads data, either by using the provided CSV files or by simulating new data given a seed and scenario, centres the longitudinal observation for stability of sampling, and fits the preliminary LMM (*linear mixed model*) and Weibull AFT models.

This file then builds the Stan data and initial values for sampling, fits the sAFT-JM model, and provides a simple comparison of results for a single fit across models.

There is guidance on which parameters to choose when generating data to match the simulation scenarios used within the manuscript.

---

### `saft_jm.stan`

Stan implementation of the sAFT-JM model.

This includes modelling of the longitudinal outcome with fixed and random effects, specifically intercept and slope, with these shared random effects joining the model within the semiparametric accelerated failure time survival model.

Bernstein polynomials are used as the flexible baseline hazard approximation, with the predictive joint log likelihood generated for capacity of diagnostics, including LOO and WAIC, for which users may use the `loo` package.

---

### `simulated_longitudinal_dataset.csv` and `simulated_survival_dataset.csv`

Simulated datasets of the longitudinal and survival data.

These can be reproduced by setting `simulate_own_data` to `TRUE` within `saft_jm_fit.R`, using:

```r
global_seed = 1
beta_2 = 0
log_AF = 0
aft_mode = "loglogistic"
lambda_c = 0
```

within the parameter settings of the `simulate_joint_dataset` function.

---

## Required packages

The required packages include:

* `cmdstanr`
* `lme4`
* `nlme`
* `survival`
* `here`
* `tidyverse`
* `MASS`

These packages may be installed by running:

```r
install.packages(c(
  "cmdstanr",
  "lme4",
  "nlme",
  "survival",
  "here",
  "tidyverse",
  "MASS"
))
```

For `cmdstanr`, the additional setup is required:

```r
cmdstanr::install_cmdstan()
```
