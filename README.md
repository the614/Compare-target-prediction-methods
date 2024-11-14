# Compare-target-prediction-methods

This repository contains the code and resources for evaluating seven target prediction methods on a shared dataset, with a focus on identifying optimal computational models for small-molecule drug repositioning. The study employs both stand-alone codes and web servers, with comparative analyses across multiple metrics to assess prediction reliability.

# Data Availability

The bioactivity data for the comparative analysis and programmatic pipeline was retrieved from the latest release of the ChEMBL 34 database (https://www.ebi.ac.uk/chembl/), updated as of March 28, 2024. This database provides extensive experimentally validated bioactivity data, including drug-target interactions, inhibitory concentrations, and binding affinities.

# Target Prediction Methods Comparison

Seven target prediction methods were compared in this study. Their prediction results are either from local codes or from web servers via crawlers.

**MolTarPred**

The MolTarPred code is based on the original source available here: http://ballester.marseille.inserm.fr/TF-benchmark.tar.gz

**Polypharmacology Browser2 (PPB2)**

PPB2 predictions were retrieved via a web crawler developed for this project: https://ppb2.gdb.tools

**RF-QSAR**

A crawler was created to access RF-QSAR predictions: https://rfqsar.kaist.ac.kr/home.php

**TargetNet**

A crawler was used to retrieve results from TargetNet: http://targetnet.scbdd.com

**ChEMBL Target Prediction**

ChEMBL’s target prediction web server was accessed via crawler: https://www.ebi.ac.uk/chembl/target-predictions

**ChEMBL Multitask Neural Network (CMTNN)**

The CMTNN predictions were obtained from https://github.com/chembl/chembl_multitask_model

**SuperPred**

The SuperPred predictions were accessed and modified using a crawler based on https://github.com/changecool/Target-Prediction-Crawler, used to fetch results from https://prediction.charite.de/subpages/target_prediction.php

# Prediction Methods Validation

The validation of prediction results includes numbers of TP, FP, TN, or FN, and several performance metrics, such as MCC, Recall, Precision and so on.
