
# Store AB Testing: Trend-Adjusted Methods

This project implements and compares robust methods for estimating the causal effect of a treatment (e.g., a marketing intervention) on store sales, with a focus on adjusting for temporal trends and pre-existing differences between stores.

## Project Structure

- `notebooks/`  
  Jupyter notebooks for all analysis steps and results comparison
- `data/`  
  Input data files (sales, features, segments, matched pairs)
- `reports/`  
  Output figures and tables

## Methods Compared

### 1. Naive Pre-Post Comparison
- Compares average sales before and after treatment for treated stores only
- **Limitation:** Does not adjust for temporal trends or external factors; likely biased

### 2. Segmentation-Based DiD (Difference-in-Differences)
- Segments stores by pre-period characteristics (e.g., using KMeans)
- Computes DiD within each segment, then aggregates
- **Use when:** You have meaningful business segments and want interpretable results

### 3. Matched DiD (Matching + DiD, Regression-Based)
- Matches each treated store to similar control stores based on pre-period features
- Computes DiD using a regression-based approach on matched data
- **Use when:** You want maximum covariate balance and robust, standard errors/confidence intervals



## Visualizations

The analysis produces several key visualizations to support interpretation and communication:

1. **Method Comparison Bar Chart:**
  - Compares estimated treatment effects (percent lift) across all methods (Naive, Segmentation DiD, Matched DiD, Overall DiD).
  - Highlights the impact of trend adjustment and methodological rigor.
  - Saved as `reports/figures/method_comparison.png`.

2. **Segments in Feature Space:**
  - Visualizes store segments (Declining, Stable, Growing) in pairwise feature space using scatter plots.
  - Helps interpret how clusters differ by pre-period slope, average sales, and volatility.
  - Saved as `reports/figures/segment_feature_space.png`.

3. **Covariate Balance Plots:**
  - Show standardized mean differences (SMD) for key features before and after matching/segmentation.
  - Demonstrate improved balance and overlap between treatment and control groups.

4. **Parallel Trends Plots:**
  - Visualize pre-period sales trends for treatment and control groups to assess the parallel trends assumption.

All figures are saved in the `reports/figures/` directory and can be used in presentations or reports to communicate results and support best practices.

## Key Analysis Steps

1. **Data Preparation:** Load and clean sales and feature data.
2. **Matching & Segmentation:**
   - Segment stores or match treatment to control stores using pre-period features.
   - Assess covariate balance before and after matching/segmentation.
3. **Diagnostics:**
   - Visualize and test the parallel trends assumption (pre-period trends).
   - Check for balance and overlap between groups.
4. **Causal Effect Estimation:**
   - **Naive:** Simple pre-post difference for treated stores (not recommended).
   - **Segmentation DiD:** Compute DiD within segments, aggregate results.
   - **Matched DiD (Regression-Based):**
     - Fit a regression: `sales ~ treatment * post` on matched data.
     - The DiD effect is the coefficient on the interaction term (`treatment:post`).
     - Use robust standard errors and confidence intervals from the regression output.
5. **Reporting:**
   - Compare all methods side-by-side.
   - Visualize treatment effects and confidence intervals.
   - Summarize key insights and best practices.

## Statistical Inference
- **Regression-based DiD** is the preferred approach for inference:
  - The t-test and confidence interval for the DiD effect are provided directly by the regression output.
  - No separate t-test or bootstrap is required for the DiD coefficient.
- **Bootstrap** is optional and only needed for custom estimators or if you want to check robustness.

## Best Practices
- Always use a control group for causal inference
- Adjust for pre-existing trends (segmentation, matching, or regression)
- Use DiD to difference out temporal confounders
- Report confidence intervals to quantify uncertainty
- Compare multiple methods to assess robustness
- Visualize and test the parallel trends assumption

## Running the Analysis
1. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn statsmodels scipy jupyter tqdm
   ```
2. Place data files in the `data/` directory.
3. Open the notebooks in `notebooks/` and run all cells in order.
4. Results and figures will be saved in the `reports/` directory.

## References
- [Difference-in-Differences (DiD)](https://en.wikipedia.org/wiki/Difference_in_differences)
- [Matching Methods](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3144483/)
- [Parallel Trends Assumption](https://www.publichealth.columbia.edu/research/population-health-methods/difference-differences)
- [Regression-Based DiD](https://www.sciencedirect.com/science/article/pii/S0304407618302112)

---
For questions or contributions, please open an issue or pull request.