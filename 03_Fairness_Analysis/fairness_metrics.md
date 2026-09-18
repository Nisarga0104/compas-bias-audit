# Fairness Metrics Analysis

## 1. False Positive Rate (FPR)

For this case, a false positive is a defendant flagged high-risk who did not reoffend.

The final assessment reports:

- Black defendants: **44.9%**
- White defendants: **23.5%**

The difference means the groups experienced different rates of this type of classification error in the published analysis.

## 2. False Negative Rate (FNR)

A false negative is a defendant flagged low-risk who did reoffend.

The final assessment reports:

- Black defendants: **28.0%**
- White defendants: **47.7%**

This is a different error pattern from FPR and illustrates why a fairness review should consider the harm associated with each error type.

## 3. Calibration / predictive parity

Calibration asks whether a given risk score corresponds to a similar observed likelihood of the outcome across groups.

The final assessment reports that Northpointe's rebuttal and independent academic work found COMPAS to be approximately calibrated across race.

## 4. Why the metrics can disagree

The project follows the formal fairness literature discussed in the final report: when groups have different base rates, a non-trivial classifier generally cannot simultaneously satisfy calibration and equalized error rates across groups, except in constrained special cases.

The governance implication is not that one metric is "the correct" metric in every context. It is that the organization must decide **which harms matter most for the use case**, document the selected fairness definition, and monitor the consequences.

## 5. Governance questions

Before deployment of a comparable high-stakes system, ask:

1. What decision is the model informing?
2. Who bears the cost of a false positive?
3. Who bears the cost of a false negative?
4. Which fairness metric corresponds most directly to those harms?
5. What trade-offs arise if another metric is prioritized?
6. Who approves the metric choice?
7. How will subgroup performance be monitored after deployment?
