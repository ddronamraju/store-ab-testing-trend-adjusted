# Store AB Testing with Trend Adjustment

## Problem Statement
Retailers often run experiments to measure the impact of new initiatives (e.g., marketing campaigns, operational changes) on store performance. However, simple pre/post comparisons can be misleading if stores have different baseline sales or trends. This project addresses the challenge of accurately estimating the causal effect of an intervention on store sales, accounting for pre-existing differences and temporal trends.

## Methodology
- **Experiment Design:**
	- Treatment and control stores were identified, with clear pre- and post-intervention periods.
- **Data Preparation:**
	- Store-level sales and pre-period features were compiled.
- **Naive Pre-Post Comparison:**
	- Simple difference in average sales before and after intervention for treatment stores only.
- **Segmentation-Based DiD (Option A):**
	- Stores were grouped by pre-period characteristics. Difference-in-Differences (DiD) was computed within each segment, then aggregated.
- **Matched DiD (Option B):**
	- Each treated store was matched to up to three control stores based on pre-period sales and trend (slope), using nearest neighbor matching without replacement. DiD was computed for matched pairs.
- **Diagnostics:**
	- Standardized mean differences (SMDs) and balance plots were used to assess pre-period comparability.
- **Uncertainty Quantification:**
	- Bootstrap resampling was used to estimate 95% confidence intervals for all methods.

## Results
- **Naive Pre-Post:**
	- Overestimated the treatment effect due to failure to account for temporal trends.
- **Segmentation-Based DiD & Matched DiD:**
	- Both trend-adjusted methods produced similar, lower estimates of lift, increasing confidence in the results.
- **Visualization:**
	- Unified plots and tables compare all methods, highlighting the importance of trend adjustment.
- **Key Insight:**
	- Controlling for pre-trend slope is critical for valid causal inference in store experiments.

## Limitations
- **Unobserved Confounding:**
	- Matching and segmentation adjust for observed features and trends, but unmeasured confounders may remain.
- **Generalizability:**
	- Results are specific to the stores and time period analyzed; effects may differ elsewhere.
- **Sample Size:**
	- Small treatment or control groups can limit statistical power and matching quality.
- **Assumptions:**
	- DiD assumes parallel trends in the absence of treatment, which may not always hold.

## Next Steps
- **Richer Feature Engineering:**
	- Incorporate additional store-level covariates (e.g., demographics, competition).
- **Alternative Methods:**
	- Explore synthetic control or regression-based approaches for further robustness.
- **Long-Term Impact:**
	- Extend analysis to measure persistence or decay of effects over time.
- **Automation:**
	- Package the workflow for scalable, repeatable analysis across experiments.

---

**For questions or collaboration, please contact the project owner.**
# Store-Level A/B Testing with Trend Segmentation and Matched Controls

This project evaluates a retail store-level A/B test using:
- pre-period sales slope for store segmentation
- trend-matched control selection
- Difference-in-Differences for causal impact estimation

Work in progress.

Quick commands:
.\.venv\Scripts\Activate.ps1s