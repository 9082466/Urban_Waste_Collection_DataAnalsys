# Waste Collection EDA and Statistical Tests – Notebook Documentation

## Overview

This notebook performs **exploratory data analysis (EDA)** and **statistical hypothesis testing** on urban waste collection data from the **Region of Waterloo**. The analysis is specifically designed to support a case study on **AI-driven demand-responsive waste routing optimization**.

---

## Purpose & Business Context

### Why This Analysis?
The Region of Waterloo currently uses **static waste collection scheduling** that does not adapt to demand variations across municipalities and neighborhoods. This analysis provides data-driven evidence that waste collection demand varies significantly by:
- Geographic location (municipality)
- Service type (residential, commercial, etc.)
- Property structure (number of units)

### Business Problem (Toyota Business Practice Method)
- **Step 1 – Problem:** Static scheduling does not adapt to changing waste demand across municipalities
- **Step 3 – Target:** Improve service reliability and reduce overflow risk
- **Step 4 – Root Cause:** Waste demand varies by municipality, service type, and housing structure
- **Step 5 – Countermeasure:** AI-driven demand-responsive routing

---

## Data Source

**File:** `Waste_Management_Collection_Addresses.csv`

### Key Variables Used

| Variable | Type | Description |
|----------|------|-------------|
| `Municipality` | Categorical | Geographic area within Region of Waterloo |
| `GarbageServiceType` | Categorical | Type of waste collection service (e.g., residential, commercial) |
| `NumberOfUnits` | Numeric | Number of dwelling/commercial units at address |
| `WasteBagLimit` | Numeric | Maximum waste bags allowed per collection cycle |

---

## Notebook Structure & Analysis

### Section 1: Dataset Overview
- Load and inspect the waste management dataset
- Display column names, data types, and basic statistics
- Identify missing values and data quality issues

### Section 2: Automatic Variable Selection
- Automatically select relevant columns for analysis
- Clean and prepare data for statistical testing
- Convert variables to appropriate data types

### Section 3: Exploratory Data Analysis (EDA)
Five key visualizations designed for non-technical stakeholders:

1. **Addresses by Municipality** – Which municipalities dominate the dataset?
2. **Addresses by Garbage Service Type** – Which service types are most common?
3. **Distribution of Waste Bag Limits** – What does waste capacity look like across the region?
4. **Waste Bag Limit by Service Type** – How does capacity vary by service structure?
5. **Number of Units vs Waste Bag Limit** – How does property density relate to capacity?

### Section 4: Statistical Test 1 – Welch's t-test

**Null Hypothesis:** Mean waste bag limit is equal between the two most common service types

**Alternative Hypothesis:** Mean waste bag limit differs between service types

**Why It Matters:** If service types have significantly different waste capacities, this supports the argument that one uniform routing logic is inefficient.

**Output Interpretation:**
- **p-value < 0.05:** Reject null hypothesis → Service types differ significantly
- **p-value ≥ 0.05:** Fail to reject → No significant difference between service types

### Section 5: Statistical Test 2 – Chi-square Test of Independence

**Null Hypothesis:** Municipality and garbage service type are independent

**Alternative Hypothesis:** Municipality and garbage service type are associated

**Why It Matters:** Association between municipality and service type suggests that service structure varies by location, supporting the need for location-specific routing strategies.

**Output Interpretation:**
- **p-value < 0.05:** Reject null hypothesis → Significant association exists
- **p-value ≥ 0.05:** Fail to reject → No significant association

**Visualization:** Heatmap showing the relationship between municipalities and service types

### Section 6: Statistical Test 3 – Pearson Correlation & Linear Regression

**Null Hypothesis:** Number of units and waste bag limit are not correlated

**Alternative Hypothesis:** Number of units and waste bag limit are correlated

**Why It Matters:** Building density and property structure drive waste collection demand. If this relationship is significant, it validates using data science and AI to predict demand and optimize routes.

**Output Interpretation:**
- **Correlation coefficient:** Strength and direction of the relationship (-1 to +1)
- **p-value < 0.05:** Relationship is statistically significant
- **R-squared:** Proportion of waste bag limit variance explained by number of units

**Visualization:** Scatter plot with regression line showing the relationship

### Section 7: Business Interpretation

**Key Takeaways:**
- Different service structures are associated with different waste capacity patterns
- Service structure varies significantly by municipality
- Property density and structure are predictive of waste capacity

**Business Implications:**
- Static scheduling is not appropriate across the region
- AI-based demand prediction and routing optimization is a valid countermeasure
- Data science can provide competitive advantage in municipal waste management

---

## How to Use This Notebook

### Prerequisites
Install required Python packages:
```bash
pip install -r requirements.txt
```

Required libraries:
- `pandas` – Data manipulation and analysis
- `numpy` – Numerical computing
- `matplotlib` – Data visualization
- `seaborn` – Statistical visualizations
- `scipy` – Statistical tests
- `scikit-learn` – Machine learning models and metrics

### Running the Notebook
1. Ensure `Waste_Management_Collection_Addresses.csv` is in the `data/` directory
2. Open the notebook: `Waste_EDA_Statistical_Tests_Aligned_EXECUTED.ipynb`
3. Run cells sequentially from top to bottom
4. Review visualizations and statistical outputs after each major section

### Key Outputs
The notebook generates:
- **EDA Visualizations:** 5 publication-ready charts
- **Statistical Test Results:** p-values, test statistics, and interpretation
- **Regression Model:** Linear model predicting waste bag limit from number of units
- **Heatmap:** Municipality vs Service Type cross-tabulation

---

## Statistical Tests Summary

| Test | Variables | Null Hypothesis | Decision Metric |
|------|-----------|-----------------|-----------------|
| **Welch's t-test** | Waste Bag Limit vs Service Type | Means are equal | p-value |
| **Chi-square** | Municipality vs Service Type | Variables are independent | p-value |
| **Pearson Correlation** | Number of Units vs Waste Bag Limit | No linear relationship | p-value, correlation coefficient |
| **Linear Regression** | Number of Units vs Waste Bag Limit | Slope = 0 | R-squared, coefficient p-value |

**Significance Level:** α = 0.05 (reject null hypothesis if p-value < 0.05)

---

## Output Files Generated

The `waste_activity_outputs/` folder contains:
- `contingency_counts.csv` – Raw contingency table (Municipality × Service Type)
- `contingency_row_percent.csv` – Row percentages from contingency table
- `data_dictionary.csv` – Metadata about variables
- `logit_odds_ratios.csv` – Odds ratios for categorical associations

---

## Key Assumptions

1. **Data Quality:** Assumes data is reasonably clean with no systematic bias
2. **Independence:** Assumes observations are independent
3. **Normality (t-test):** Welch's t-test is robust to non-normality with large samples
4. **Chi-square:** Assumes expected frequencies ≥ 5 in most cells
5. **Regression:** Assumes linear relationship; residuals approximately normally distributed

---

## Limitations & Considerations

- **Static Data:** Analysis is point-in-time; seasonal variations are not captured
- **Missing Values:** Rows with missing key variables are excluded from analysis
- **Causation:** Statistical association does not imply causation
- **Generalization:** Results specific to Region of Waterloo; may not generalize to other municipalities
- **Outliers:** Analysis includes extreme values; consider robust methods if outliers are problematic

---

## Business Applications

### Immediate Use Cases
1. **Stakeholder Communication:** Present findings to municipal leadership
2. **Route Optimization:** Use demand predictions to improve collection schedules
3. **Resource Allocation:** Allocate collection vehicles based on predicted demand
4. **Service Planning:** Identify high-variability areas requiring flexible scheduling

### Product Development
- **AI/ML Tool:** Build demand-prediction model using these insights
- **Market Opportunity:** Sell demand-responsive routing software to municipalities
- **Competitive Advantage:** Data-driven optimization reduces operational costs

---

## Author & Context

- **Course:** Case Studies in AI (Conestoga College)
- **Program:** WED-MORN (Level 2)
- **Case Study:** Urban Waste Collection Optimization for Region of Waterloo
- **Analysis Method:** Toyota Business Practice (TBP) + Data Science

---

## Questions or Modifications?

To customize this analysis:
- **Add variables:** Modify column selection in Section 2
- **Change test variables:** Update `municipality_col`, `service_col`, `units_col`, `bag_limit_col`
- **Adjust significance level:** Change threshold from 0.05 to alternative value (e.g., 0.01 for stricter testing)
- **Expand tests:** Add additional statistical tests (e.g., ANOVA, logistic regression)

---

## References

- TBP Methodology: Toyota Business Practice structural problem-solving
- Statistical Tests: Scipy documentation (https://docs.scipy.org/doc/scipy/reference/stats.html)
- Data Visualization: Seaborn documentation (https://seaborn.pydata.org/)