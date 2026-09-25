# College Student Dropout Prediction

Semester machine learning project by **Boyett and Etzler**.

## Objective

Predict whether a student will be classified as **Dropout**, **Enrolled**, or **Graduate** at the end of the normal program duration using admission, prior education, and demographic information available at enrollment.

The project will explore whether predictions can help academic advisers identify students who may benefit from tutoring, financial guidance, or academic planning. Predictions are intended to guide supportive outreach.

## Dataset

- **Name:** Predict Students' Dropout and Academic Success
- **Source:** https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success
- **License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Size:** 4,424 student records and 37 columns: 36 predictors and `Target`
- **Unit of observation:** One undergraduate student
- **Target counts:** Dropout: 1,421; Enrolled: 794; Graduate: 2,209
- **Missingness:** No blank/null cells in the downloaded file. Some categorical fields include explicit unknown or blank codes.

The data describe students at the Polytechnic Institute of Portalegre, Portugal. The dataset combines institutional records, national admission information, and macroeconomic data. The published data descriptor explains collection and outcome definitions: https://doi.org/10.3390/data7110146.

Counts and missingness were verified against the UCI download on September 25, 2026. The feature inventory is in `docs/feature_inventory_BoyettEtzler.xlsx`.

## Milestone 1 documents

- [Proposal](docs/Proposal_BoyettEtzler.pdf)
- [Team contract](docs/BoyettEtzler_Contract.pdf)
- [Feature inventory](docs/feature_inventory_BoyettEtzler.xlsx)

The PDFs are preserved as supplied by the team. Correction to the proposal's target-distribution text: the Dropout count is **1,421**, not 1,412. The correct total is 4,424 students.

## Setup

Use Python 3 in a virtual environment, then install the project packages:

```sh
python -m venv .venv
```

Activate the environment:

```powershell
# Windows PowerShell
.venv\Scripts\Activate.ps1
```

```sh
# macOS or Linux
source .venv/bin/activate
```

```sh
python -m pip install -r requirements.txt
```

Download the dataset ZIP from the UCI source above, extract `data.csv`, and place it in `data/raw/`. Read the file using a semicolon separator:

```python
import pandas as pd

df = pd.read_csv("data/raw/data.csv", sep=";")
df.columns = df.columns.str.strip()
```

## Repository structure

```text
data/raw/          Downloaded source data (excluded from Git)
data/processed/    Prepared data (excluded from Git)
docs/              Project documents and feature inventory
notebooks/         Exploration and modeling notebooks
src/               Reusable project code
requirements.txt   Initial Python dependencies
```

## What success looks like

Our model will be useful if it helps academic advisers identify students who may drop out early enough to offer support, such as tutoring, financial guidance, or academic planning. We will assess whether its predictions match students' recorded outcomes on data it has not seen before and whether it identifies students who need attention without overwhelming advisers with unnecessary alerts. A useful prediction would prompt a supportive conversation, not label a student as certain to fail. Missing a student who later drops out would generally be more harmful than incorrectly flagging a student who stays enrolled, because the missed student could lose an opportunity to receive help. However, unnecessary alerts could waste advisers' time or worry students, so predictions should guide careful, respectful outreach.

## Risks

1. **Using information unavailable at enrollment.** Semester grades and course completion records could make predictions appear more accurate even though advisers would not have that information when students first enroll. We will exclude semester results from the enrollment model and use other variables only when their availability at enrollment can be verified.
2. **Limited generalizability and potential bias.** The dataset represents historical students at one institution in Portugal, so patterns may not apply to students at other colleges or today. Demographic information could also produce uneven prediction quality across student groups. We will examine these differences where sample sizes allow and treat predictions as guidance for supportive outreach rather than grounds for restricting opportunities.

## Project status

Milestone 1: problem definition, dataset verification, and feature inventory. Model development and evaluation have not yet been completed.

## Dataset attribution

Realinho, V., Vieira Martins, M., Machado, J., & Baptista, L. (2021). *Predict Students' Dropout and Academic Success* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89.

Dataset license: https://creativecommons.org/licenses/by/4.0/. This license applies to the source dataset; no separate license for this repository's original work has been selected.
