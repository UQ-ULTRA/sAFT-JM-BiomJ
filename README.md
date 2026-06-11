# Bayesian joint modelling using semiparametric accelerated failure time approaches
## Model fitting example and guide

This repository contains code to generate data and fit the models proposed and discussed within the Biometrical Journal submission paper titled 'Bayesian joint modelling using semiparametric accelerated failure time approaches'. The goal of this paper pertained to the development of the novel sAFT-JM (semiparametric accelerated failure time joint model) framework with the use of Bernstein Polynomials (BPs) for flexible baseline hazard specification, with simulation studies demonstrating parameter recovery in a joint modelling context across an array of data generation scenarios. In this file we show the key programs used as components for our simulation study in a minimal form, for the purpose of comprehensibility.

#### datagen.R

The file containing functions relevant for data generation. The key function 'simulate_joint_dataset' generates joint longitudinal and survival datasets with individual-level random effects. This real-world inspired data generation scheme assigns participants to an equal size of each treatment, with options for users to choose between log-logistic or weibull true baseline hazards, censoring proportions (administrative, none or 50% censoring) and treatment effects. We list 

#### saft_jm_fit.R

Primary file for fitting the proposed sAFT joint model. This first loads data (either by using the provided CSV files or by simulating new data given a seed and scenario), centres the longitudinal observation (for stability of sampling), fits the preliminary LMM (linear mixed model) and Weibull AFT models. This file then builds the Stan data and initial values for sampling, fits the sAFT-JM model and provides simple comparison of results for a single fit across models.

#### saft_jm.stan



### simulated_longitudinal_dataset.csv and simulated_survival_dataset.csv 

Simulated datasets of the longitudinal and survival data. These can be reproduced through by setting 'simulate_own_data' to TRUE within 'saft_jm_fit.R' and then using 'global_seed=1', using 'scenario 1,


## Required packages

The packages required 
