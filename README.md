

# Yulu Bike-Sharing Demand Analysis: End-to-End Pipeline

## 📌 Project Overview

This project is a complete data science pipeline designed to answer business questions for **Yulu**, a micro-mobility and bike-sharing company. Yulu has experienced dips in revenue and wants to understand the underlying factors driving the demand for their electric bicycles.

Unlike standard tutorials with perfect data, this project simulates a **highly realistic, "messy" dataset** with 100,000 rows. The script guides the data through a rigorous cleaning pipeline before applying hypothesis testing and Multiple Linear Regression to extract actionable, statistically significant business insights.

## ⚙️ Features & Workflow

The main Python script is divided into four distinct phases:

### Phase 0: Synthetic "Unclean" Data Generation

To mimic real-world data engineering challenges, the script generates a dataset and intentionally injects the following data quality issues:

* **Missing Values (NaNs):** Missing target variables (`count`) and features.
* **Sensor Errors / Outliers:** Impossible values like windspeed at `999.0` or humidity at `-25.0`.
* **Mixed Data Types:** The `weather` column contains a mix of integers and strings (e.g., `"Sunny"`).
* **Invalid Categories:** The `season` column contains non-existent seasons (e.g., season `5`).
* **Duplicates:** 1,000 perfectly duplicated rows shuffled into the dataset.

### Phase 1 & 2: Diagnostic & Cleaning Pipeline

A robust `pandas` pipeline that prepares the data for statistical modeling:

* **Target Isolation:** Drops rows where the dependent variable (`count`) is missing (never impute the target).
* **Robust Imputation:** Neutralizes extreme outliers by converting them to `NaN`, then imputes missing environmental features using the **median** to resist skewness.
* **Type Coercion & Deduplication:** Cleans strings into valid categories, removes duplicates, and ensures strict integer types for discrete variables.

### Phase 3: Hypothesis Testing & Confidence Intervals

Using `scipy.stats`, the script performs statistical tests to establish baseline relationships, including **95% Confidence Intervals (CI)** for expected bike demand across groups:

* **Two-Sample T-Test:** Compares demand on Working days vs. Non-Working days.
* **One-Way ANOVA:** Tests for statistically significant variances in demand across different Seasons and Weather conditions.

### Phase 4: Multiple Linear Regression (OLS)

Using `statsmodels`, the script fits an Ordinary Least Squares (OLS) regression model to answer Yulu's core business questions:

1. **Which variables are significant?** (Filters for $p$-values $< 0.05$).
2. **What is their expected impact?** (Calculates the coefficient and 95% CI for every significant variable).
3. **How well does the model explain demand?** (Calculates the Adjusted $R^2$ score).

---

## 🛠️ Dependencies

To run this pipeline, you will need Python 3.x and the following libraries:

* `pandas` (Data manipulation)
* `numpy` (Numerical operations)
* `scipy` (Hypothesis testing)
* `statsmodels` (Linear regression & statistical modeling)

You can install the requirements via pip:

```bash
pip install pandas numpy scipy statsmodels

```

## 🚀 How to Run

1. Clone this repository or download the Jupyter Notebook (`.ipynb`).
2. Open the notebook in **Jupyter Notebook** or **JupyterLab**.
3. Run the cells from top to bottom to execute the analysis.



3. The script will output console reports in sequence: Data Diagnostics -> Cleaning Shape Changes -> Hypothesis Test Results -> OLS Regression Summary.

## 📊 Business Value / The "So What?"

This pipeline doesn't just output raw math; it formats the outputs for business stakeholders. By utilizing 95% Confidence Intervals, Yulu executives won't just learn that "temperature matters"—they will learn exactly *how many* extra bicycles they can expect to rent out for every 1-degree rise in temperature, allowing for precise inventory and revenue forecasting.
