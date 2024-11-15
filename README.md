# Compare-target-prediction-methods

This repository contains code and resources for evaluating seven target prediction methods on a shared dataset, with a focus on identifying optimal computational models for small-molecule drug repositioning. The study integrates both standalone code implementations and web-server-based methods, enabling a comparative analysis across multiple metrics to assess prediction reliability.


# Steps

The repository is organized into four main folders: ChEMBL Database, Query, TF Methods Comparison, and Validation.


**1.	ChEMBL Database:**

The bioactivity data for the comparative analysis and programmatic pipeline was retrieved from the latest release of the ChEMBL 34 database (updated as of March 28, 2024), providing experimentally validated bioactivity data, including drug-target interactions, inhibitory concentrations, and binding affinities.

**Process:**

•	**Download:** Obtain the latest data from https://www.ebi.ac.uk/chembl/.

•	**Database Setup:** Load ChEMBL database files into PostgreSQL for local data access.

•	**Data Extraction:** Retrieve and filter data to extract SMILES strings, ChEMBL IDs, and target IDs, then format and output a CSV file with columns for ChEMBL IDs, SMILES, and Target IDs.


**2.	Query:**

The query step prepares a benchmark dataset of FDA-approved drugs from ChEMBL to serve as query molecules for target prediction.

**Process:**

•	**Data Collection:** Collect FDA-approved molecules and exclude them from the main dataset to avoid prediction overlap.

•	**Sampling:** Randomly select 100 FDA-approved drugs as query molecules.

•	**Data Organization:** Store the selected samples in two CSV files within this folder: one with the 100 query molecules and another with the remaining molecules.


**3.	TF Methods Comparison:**

Seven target prediction methods were compared in this study. Prediction results were generated either from stand-alone codes or web-server crawlers.

•	**MolTarPred:** Used local code based on the original source http://ballester.marseille.inserm.fr/TF-benchmark.tar.gz

•	**Polypharmacology Browser2 (PPB2):** Retrieved predictions by webcrawler from https://ppb2.gdb.tools

•	**RF-QSAR:** Access predictions by webcrawler from https://rfqsar.kaist.ac.kr/home.php

•	**TargetNet:** Obtained results by webcrawler from http://targetnet.scbdd.com

•	**ChEMBL Target Prediction:** Accessed by webcrawler from https://www.ebi.ac.uk/chembl/target-predictions

•	**ChEMBL Multitask Neural Network (CMTNN):** Download from https://github.com/chembl/chembl_multitask_model and run locally

•	**SuperPred:** Accessed and modified by a webcrawler based on https://github.com/changecool/Target-Prediction-Crawler, fetched results from https://prediction.charite.de/subpages/target_prediction.php

**Process:**

•	**Predictions:** Execute local codes for MolTarPred and CMTNN, and run web crawlers for PPB2, RF-QSAR, TargetNet, ChEMBL, and SuperPred.

•	**Output:** CSV files in a standardized format for each method.


**4.	Validation:**

The validation step evaluates prediction accuracy by calculating True Positives (TP), False Positives (FP), True Negatives (TN), and False Negatives (FN), alongside performance metrics like Matthews Correlation Coefficient (MCC), Recall, and Precision.

**Process:**

•	**Metric Calculation:** For each query molecule, calculate TP, FP, TN, and FN counts, along with individual performance metrics.

•	**Comparison:** Evaluate the methods by average performance metrics across all 100 queries.
