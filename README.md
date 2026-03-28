# Hospital Readmission Analysis

Exploratory analysis of diabetic patient readmissions using the UCI Diabetes 130-US Hospitals dataset (1999–2008). The goal was to find what patient and clinical factors are associated with being readmitted within 30 days.

---

## What's in here

- `hospital_readmission_analysis.ipynb` — full analysis notebook (data loading → cleaning → EDA → findings)
- `analysis_report.md` — written summary of key findings
- `data_dictionary.txt` — what each column in the dataset means
- `visualizations/` — all charts saved as PNG files

---

## Dataset

100,000+ patient encounters across 130 US hospitals. Source: [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008)

The dataset uses `?` for missing values and has several columns with very high missingness (weight: 97%, medical specialty: 49%). Cleaning that up was a big part of the work.

---

## How to run

```bash
pip install pandas numpy matplotlib seaborn scipy ucimlrepo notebook
jupyter notebook hospital_readmission_analysis.ipynb
```

The notebook downloads the dataset automatically via `ucimlrepo`. No manual download needed.

---

## Key findings

- Overall 30-day readmission rate: ~11%
- Prior inpatient visits are the strongest predictor of readmission
- Patients on more medications have higher readmission rates — reflects disease complexity
- Middle-aged patients (40–70) account for most encounters and readmissions
- Longer hospital stays correlate with slightly higher readmission risk
