# Compare-target-prediction-methods
A comparative study of seven ligand-centric target prediction methods using FDA-approved drugs. This repository provides the full pipeline to evaluate and validate prediction accuracy across standalone models and webserver-based approaches, with a focus on small-molecule drug repositioning.

To learn more about the study, see the corresponding manuscript[1] and the original benchmarking paper[2].

## Repository Structure
```text
ChEMBL_Database/           # Step 1	Prepare ChEMBL Database
├── 01_Chembl_34_all                    # Step 1.1–1.2
├── 02_Chembl_34_filter                 # Step 1.3
├── 03_Chembl_34_database               # Step 1.3
├── 04_database_10nM                    # Step 1.3–1.4
└── 05_High-confidence_filter           # For MolTarPred_high-confidence.py

Query/                     # Step 2	Select Query Molecules
├── 01_Query_FDA                        # Step 2.1
└── 02_Random_100_query                 # Step 2.2

TF_Methods_Comparison/     # Step 3 Run Target Prediction Methods
├── 01_Initial MolTarPred
├── 02_PPB2
├── 03_RF-QSAR
├── 04_TargetNet
├── 05_ChEMBL
├── 06_CMTNN
├── 07_SuperPred
├── 08_MolTarPred_high-confidence
├── 09_MolTarPred_fingerprints&similarity
└── query_10nM.csv        # Query selected by Step 2 and tested for Step 3 & 4

Validation/               # Step 4 Validate Prediction Performance
├── 01_Top5 or 10
├── 02_High-confidence filter
├── 03_Fingerprints&similarity
└── query_10nM.csv        # Query selected by Step 2 and tested for Step 3 & 4

requirements.txt          # Python dependencies
```

## Installation

Install Python dependencies:
```bash
pip install -r requirements.txt
```
Install RDKit (required for ChEMBL processing):
```bash
conda install -c conda-forge rdkit==2024.03.04
```
System prerequisites:
- [PostgreSQL 16.3](https://www.postgresql.org/download/)
- [pgAdmin4 8.6](https://www.pgadmin.org/download/)


## Methods Overview
Seven target prediction methods were compared in this study. Prediction results were generated either from standalone code or web-server crawlers.


| Method                                                                  | Type                   | 
| ----------------------------------------------------------------------- | ---------------------- |
| [MolTarPred](http://ballester.marseille.inserm.fr/TF-benchmark.tar.gz)  | Stand-alone code    |
| [PPB2](https://ppb2.gdb.tools)                                          | Web-server crawler | 
| [RF-QSAR](https://rfqsar.kaist.ac.kr/home.php)                          | Web-server crawler |
| [TargetNet](http://targetnet.scbdd.com)                                 | Web-server crawler |
| [ChEMBL](https://www.ebi.ac.uk/chembl/target-predictions)               | Web-server crawler |
| [CMTNN](https://github.com/chembl/chembl_multitask_model)               | Stand-alone code   |
|[SuperPred](https://prediction.charite.de/subpages/target_prediction.php)| Web-server crawler |


## Outputs
All predictions are standardized as CSV files with the following format:
- Ligand-id: Compound ID (without "CHEMBL" prefix)
- SMILES: Canonical SMILES
- Target-id: Colon-separated target IDs (without "CHEMBL" prefix)

## Instructions

### Step 1: Prepare ChEMBL Database
- **1.1**  Download the ChEMBL PostgreSQL Database (`postgresql.tar.gz`) from [ChEMBL Downloads](https://www.ebi.ac.uk/chembl/downloads).
- **1.2**  Restore to PostgreSQL using pgAdmin4 locally.
- **1.3**  Extract and filter data:
  - Only keep IC50, Ki, or EC50 values ≤ 10,000 nM
  - Confidence score ≥ 7
  - Single-target records only
- **1.4**  Remove:
  - Targets containing `"complex"`, `"multiple"`, or `"unknown"`
  - Duplicate compound–target pairs
- **1.5**  Save outputs as `.csv` files.

---

### Step 2: Select Query Molecules
- **2.1**  Filter FDA-approved molecules.
- **2.2**  Randomly sample 100 FDA-approved drugs.
- **2.3**  Store in CSV files:
  - `query_10nM.csv`: A random sample of 100 FDA-approved molecules.
  - `database_10nM_high-confidence.csv`: Remaining molecules used as potential ligands.

---

### Step 3: Run Target Prediction Methods
- **3.1**  Execute local models or use automated web crawlers to run server-based models.
- **3.2**  Export all results in a standardized format.

---

### Step 4: Validate Prediction Performance
- **4.1**  For each query compound:
  - Calculate TP, FP, TN, FN
  - Compute performance metrics: Accuracy, Recall, Precision, Specificity, and MCC
- **4.2**  Compare methods using average metrics across the 100 queries.


## Software Versions

| Tool               | Version    |
| ------------------ | ---------- |
| Python             | 3.11.5     |
| PostgreSQL         | 16.3       |
| pgAdmin4           | 8.6        |
| RDKit              | 2024.03.04 |
| scikit-learn       | 1.2.0      |
| requests           | 2.32.2     |
| BeautifulSoup4     | 4.12.3     |
| pandas             | 2.2.2      |
| numpy              | 1.26.4     |
| selenium           | 4.22.0     |
| webdriver\_manager | 4.0.2      |
| SQLAlchemy         | 2.0.30     |
| ONNX Runtime       | 1.18.1     |
| aiohttp            | 3.9.5      |
| nest\_asyncio      | 1.6.0      |


You can also replicate the environment with:
```bash
pip install -r requirements.txt
```

## Citation
If you use this repository, please cite:
1. He T., Caba, K., Ballester P.J. (2025). A precise comparison of molecular target prediction methods. Digital Discovery.
Preprint: https://chemrxiv.org/engage/chemrxiv/article-details/6823d11e50018ac7c507fd3d
2. Peon A., Dang C., Ballester P.J. (2016). How reliable are ligand-centric methods for target fishing? Frontiers in Chemistry 4:15.
https://doi.org/10.3389/fchem.2016.00015
