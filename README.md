# 🏥 Hospital Readmission Analysis

A hospital readmission within 30 days is expensive and, in a lot of cases,
preventable — which is exactly why CMS penalizes hospitals for it. This is
an exploratory analysis of 100,000+ diabetic patient encounters across 130
US hospitals (1999–2008), digging into which patient and clinical factors
actually associate with a patient coming back within 30 days, versus which
ones look predictive but don't hold up once you account for what's actually
driving them.

## 🧹 The real work was the cleaning, not the charts

The dataset uses `?` for missing values, and three columns were unusable as-is:
`weight` (97% missing), `medical_specialty` (49% missing), `payer_code`
(40%+ missing). All three were dropped rather than imputed — filling in a
97%-missing column with any strategy would be manufacturing signal that
isn't there, not preserving it. Getting the missingness picture right before
touching a single correlation was the actual prerequisite for trusting
anything downstream — see `missing_values.png` for the full picture.

## 📊 What actually predicts readmission

- **Prior inpatient visits is the strongest single predictor.** Patients
  already hospitalized before are noticeably more likely to come back within
  30 days — clinically this tracks: it's identifying a population with
  complex, recurring conditions, not a coincidental correlation.
- **Medication count correlates with readmission — but likely as a proxy,
  not a cause.** More medications tends to mean more severe disease burden,
  not that the medications themselves are driving readmission. Worth
  stating plainly because it's the kind of number that gets misread as
  causal in a quick read.
- **Age isn't monotonic.** 40–70 accounts for the bulk of both encounters
  and readmissions, but the oldest bracket (80–90+) doesn't show the highest
  readmission rate you'd naively expect — plausibly discharge planning,
  palliative care decisions, or survival bias in who even shows up in this
  dataset at all. Flagged as a hypothesis, not a conclusion — the dataset
  alone can't distinguish between those explanations.
- **Longer stays, more diagnoses, both trend upward** with readmission risk
  — consistent with the same complexity-of-care thread underneath the
  medication-count finding.

Full writeup with the actual numbers: [`analysis_report.md`](analysis_report.md).

## ⚠️ What this analysis can't tell you

Worth being upfront about before anyone reads too much into a chart:

- **Correlation, not causation.** Longer stays and higher medication counts
  most plausibly reflect *sicker patients*, not readmission-causing
  treatments — nothing here is a controlled comparison.
- **Same-hospital-network readmissions only.** A patient readmitted at a
  *different* hospital doesn't show up as a readmission in this data — the
  true rate is very likely higher than the ~11% observed here.
- **1999–2008 data.** Diabetes treatment guidelines and medication options
  have moved on substantially since — patterns here are historical, not a
  claim about current clinical practice.
- **Class imbalance.** ~11% positive class — any predictive model trained
  on this needs to account for that explicitly (class weighting, resampling,
  or a metric other than raw accuracy), or it'll learn to just predict "no"
  and look deceptively accurate doing it.

## 🚀 Running it

```bash
pip install pandas numpy matplotlib seaborn scipy ucimlrepo notebook
jupyter notebook hospital_readmission_analysis.ipynb
```

The notebook pulls the dataset itself via `ucimlrepo` — no manual download.
Full column-by-column meaning (including the medication dose-change columns
and the derived binary target) is in
[`data_dictionary.txt`](data_dictionary.txt).

## 📁 Repository structure

```
├── hospital_readmission_analysis.ipynb  # full analysis: load -> clean -> EDA -> findings
├── analysis_report.md                    # written summary with the actual numbers
├── data_dictionary.txt                   # every column, what it means, what got dropped and why
└── visualizations/                       # every chart referenced above, as PNGs
```

## Source

[UCI Diabetes 130-US Hospitals dataset](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008), 1999–2008.
