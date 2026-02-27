# BrainGML®-AD — Paper Results Repository

This repository provides the **analysis artifacts and subject-level outputs** used to generate the main results reported in the BrainGML®-AD manuscript, focusing on:

1) **Primary endpoint outputs** against an autopsy reference standard (AD neuropathologic change; ADNC) defined by the **ABC** scoring categories;  
2) **Exploratory neuropathologic staging associations** between **synthetic CSF biomarkers** (Aβ42, pTau181, total Tau, and derived ratio) and neuropathology scales (**ABC, Thal, Braak, CERAD**).

> This repository is intended to support reproducibility of the manuscript’s *reported results* (tables/figures) and does not provide any clinical decision support tool.

---

## Contents

### Data tables (subject-level outputs)
- `data/primary_endpoint_subject_level.csv`  
  Subject-level outputs for the primary endpoint analyses:
  - autopsy reference labels (ABC category; ADNC binary label)
  - synthetic biomarker ratio (continuous) used for ROC/AUC
  - device three-class output (AD / non-AD / grey-zone) and definitive-call indicator

- `data/staging_subject_level.csv`  
  Complete-case subset used for exploratory staging analyses:
  - neuropathology scales (ABC, Thal, Braak, CERAD; raw variables when available)
  - synthetic biomarkers (Aβ42, pTau181, total Tau, ratio)
  - minimal covariates used in adjusted models (age, sex)

### Figures
- `figures/` contains rendered figures used in the manuscript (e.g., ROC curves, forest plots).

### Scripts
- `scripts/` contains minimal scripts to reproduce key outputs (CSV generation and core analyses).

---

## Key definitions (as used in the manuscript)

### Autopsy reference standard (ADNC)
- `abc_category` is one of: `Not`, `Low`, `Intermediate`, `High`.
- `adnc_label` is defined as:
  - `1` (ADNC positive) if `abc_category ∈ {Intermediate, High}`
  - `0` (ADNC negative) if `abc_category ∈ {Not, Low}`

### Three-class output and “grey-zone”
- `bgml_call ∈ {AD, non-AD, grey-zone}`.
- Sensitivity/specificity are computed **only on definitive calls** (grey-zone excluded), consistent with the manuscript.
- ROC/AUC is computed using the **continuous synthetic pTau181/Aβ42 ratio** (grey-zone included, as it is a score-based analysis).

---

## How to reproduce the manuscript numbers

### 1) Primary endpoint (autopsy cohort)
Compute sensitivity and specificity on definitive calls:
- ADNC+ (ABC Intermediate/High) vs ADNC− (ABC Not/Low)

### 2) ROC/AUC
Compute AUC using the continuous synthetic ratio:
- `y = adnc_label`
- `score = bgml_ratio`

### 3) Exploratory staging associations
Fit proportional-odds ordinal logistic regression models for each staging scale:
- outcomes: `ABC`, `Thal`, `Braak`, `CERAD` (ordinal)
- predictors: synthetic Aβ42, pTau181, ratio (standardised; per 1 SD)
- covariates: age and sex (adjusted models)

---

## Data provenance and identifiers

This repository contains **subject-level derived outputs** used in the manuscript.  
All subject identifiers are **pseudonymised**. No direct identifiers (names, dates of birth, clinical free text, imaging files) are included.

If your analysis requires access to raw NACC/ADNI data, please follow the corresponding data access procedures.

---

## Citation

If you use these materials, please cite:

> [Full manuscript citation — add once accepted/published]
> BrainGML®-AD manuscript title, journal, year, DOI.

---

## License

- Code in `scripts/` is released under the **MIT License** (see `LICENSE`).
- Data tables in `data/` are released under **CC BY-NC 4.0** unless otherwise stated.
- Any third-party datasets remain governed by their original data use agreements.

---

## Contact

For questions regarding the repository or reported results:
- Félix Renard, GeodAIsics  or Arnaud Attyé, GeodAIsics
- felix@geodaisics.com or arnaud@geodaisics.com
