# Hospital Readmission Analysis — Key Findings

## Overview

This analysis looks at 100,000+ diabetic patient encounters across 130 US hospitals between 1999 and 2008, focusing on what drives 30-day readmissions. The dataset came with significant data quality issues — ~97% of weight values were missing, and columns like `medical_specialty` and `payer_code` were over 40% empty — so the first priority was cleaning before any analysis could be trusted.

## Readmission Patterns

The overall 30-day readmission rate sits around 11%. Prior inpatient visits turned out to be the strongest predictor — patients who had been hospitalized before were noticeably more likely to return within 30 days, which makes clinical sense. These are patients with complex, recurring conditions. Number of medications was also positively correlated with readmission, likely because higher medication counts reflect more severe disease burden rather than medications themselves causing readmissions.

## Clinical Observations

Patients aged 40–70 make up the bulk of encounters and show readmission rates at or above the overall average. Contrary to what you might expect, the oldest patients (80–90+) don't always have the highest readmission rates — this could reflect differences in discharge planning, palliative care decisions, or survival bias in the dataset. Average length of stay was slightly higher for readmitted patients, and patients with more recorded diagnoses trended toward higher readmission rates, reinforcing the complexity-of-care hypothesis.

## Limitations

This data is from 1999–2008, so treatment guidelines and medication options have changed substantially since then. The dataset only captures readmissions to the *same* hospital network, meaning the true readmission rate is likely higher. Correlation here doesn't imply causation — longer stays and more medications may reflect sicker patients, not causes of readmission. Any predictive model built on this data would need to account for significant class imbalance (~11% positive class) and potential temporal drift.
