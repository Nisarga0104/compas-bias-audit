# Fairness Control Matrix

| ID | Control | Purpose | Owner | Evidence | Timing |
|---|---|---|---|---|---|
| F-01 | Pre-deployment subgroup performance testing | Detect material subgroup disparities before go-live | AI Risk / Model Risk | Evaluation report | Pre-deployment |
| F-02 | Document fairness-metric selection | Make the fairness definition auditable | AI Governance Committee | Decision record | Before approval |
| F-03 | Independent validation | Reduce reliance on vendor-only validation | Risk / Independent Validator | Validation report | Before approval |
| F-04 | Threshold and use-case review | Assess consequences of false positives and false negatives | Business + Risk | Threshold analysis | Before approval |
| F-05 | Human oversight | Preserve accountable human review for high-impact decisions | Business Owner | Override / review records | Continuous |
| F-06 | Contest / appeal mechanism | Give affected people a route to challenge an outcome | Operations / Compliance | Appeal records | Continuous |
| F-07 | Ongoing subgroup monitoring | Detect performance changes over time | Risk / Model Risk | Monitoring dashboard/report | Periodic |
| F-08 | Data/outcome review | Identify limitations in labels and outcome measurement | Data / Risk | Data-quality assessment | Periodic |
| F-09 | Material-change reassessment | Prevent fairness assumptions becoming stale after model/data changes | AI Governance Committee | Change assessment | Event-driven |

## Control principle

No individual metric or control should be treated as proof that a high-stakes AI system is fair. Controls should operate as a layered governance process.
