# Nocturnal Hypoxemia and Intraoperative Hemodynamics in Bariatric Surgery

This repository contains the final analytical report for **BIOSTAT 705**. The project utilizes retrospective clinical data to investigate the relationship between severe obstructive sleep apnea (OSA) and cardiovascular stability during laparoscopic bariatric procedures. 

## 📌 Project Overview
Severe nocturnal hypoxemia is a hallmark of OSA and is closely linked to cardiovascular dysfunction. This analysis focuses on determining if the severity of preoperative hypoxemia predicts intraoperative hypotension, and whether metabolic comorbidities (specifically diabetes) modify this physiological response.

**Primary Research Question:** Is there an independent association between the percentage of sleep time spent at SaO2 < 90% and intraoperative time-weighted average mean arterial pressure (TWA MAP), and does a comorbid diabetes diagnosis modify this relationship?

## 📂 Data Source
The data is derived from a retrospective clinical cohort of patients undergoing laparoscopic bariatric surgery.
* **Key Variables:**
    * **Outcome Variable:** Intraoperative TWA MAP (continuous, mmHg).
    * **Primary Predictor:** Nocturnal Hypoxemia (continuous, % of sleep time spent at SaO2 < 90%).
    * **Effect Modifier:** Diabetes Diagnosis (categorical: Yes/No).
    * **A Priori Confounders:** Age, BMI, biological sex, race, smoking status, hypertension, coronary artery disease (CAD), preoperative antihypertensive medications, CPAP therapy adherence, and type of bariatric surgery.

## 📊 Methodology
The analysis was conducted in **R** using R Markdown. To maintain a rigorous Family-Wise Error Rate across the two primary aims, a Bonferroni-corrected significance threshold of α = 0.025 was strictly applied. The statistical workflow included:

1. **Assumption Diagnostics & Model Selection:** * Component+Residual (CR) plots to visually assess linearity.
   * Likelihood Ratio Tests (LRT) and AIC comparisons evaluating a standard multivariable linear model against a Linear Spline (knot at 15%) and a Restricted Cubic Spline (df = 4).
2. **Aim 1 Analysis (Main Effect):** * Multivariable Linear Regression to estimate the adjusted marginal effect of sleep time on TWA MAP.
3. **Aim 2 Analysis (Effect Modification):** * Inclusion of a `sleeptime * diabetes` interaction term.
   * Partial F-Test (ANOVA) to assess interaction significance.
   * Stratified marginal effect estimation utilizing the `ggeffects` and `emmeans` packages to quantify the impact of a 25% absolute increase in severe sleep time (50% to 75%).

## 🔑 Key Findings
* **No Main Effect:** After adjusting for clinical confounders, the percentage of sleep time spent at SaO2 < 90% was not independently associated with overall intraoperative TWA MAP. 
* **Diverging Clinical Trends:** The interaction between diabetes and severe sleep time exhibited a clinically compelling trend that narrowly missed the strict Bonferroni threshold (F = 4.938, p = 0.027).
* **Stratified Hemodynamic Impact:** A modeled 25% absolute increase in sleep time (from 50% to 75%) resulted in divergent outcomes based on comorbidity status. Non-diabetic patients exhibited a non-significant 0.73 mmHg increase in expected TWA MAP, whereas diabetic patients exhibited a marked 2.48 mmHg decrease in expected TWA MAP (95% CI: -4.77 to -0.19).
* **Methodological Limitations:** Model precision at extreme hypoxemic thresholds was limited by heavy right-skewness in the exposure data, highlighting the need for targeted, high-severity prospective cohorts in future research.

## 🛠️ Dependencies & Usage
To reproduce this analysis, clone the repository and open the R Markdown file. Ensure the raw dataset is located in the working directory before knitting. 

**Required R Packages:**
```r
install.packages(c("tidyverse", "gtsummary", "ggplot2", "patchwork", "ggeffects", "emmeans", "lmtest", "lspline", "flextable"))
