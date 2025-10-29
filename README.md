# Unemployment in India: Integrated Data Analysis Project

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

This project integrates, validates, and analyzes unemployment data from India across two complementary datasets to produce actionable insights into labor market trends during 2019–2020. The work is structured into **three comprehensive reports**, each serving a distinct purpose in the data-to-insight pipeline.

---

## 📑 The Three Reports

### 1. **Data Quality Report**  
*Focus: Data integrity, completeness, and reliability*

- Confirmed **zero missing values** and **no duplicate records** in the final merged dataset (1,007 rows).
- Validated **plausible ranges** for key metrics:
  - Unemployment Rate: 0% – 76.74% (mean: 11.91%)
  - Estimated Employed: ~49K – 59.4M
  - Labour Participation Rate: 13.33% – 72.57%
- Identified minor issues:
  - `Date` column initially stored as string (resolved via `pd.to_datetime`)
  - One potential outlier (76.74% unemployment) warrants contextual review
- Verified geographical and categorical consistency across 28 regions and 5 area types.

✅ **Conclusion**: The dataset is clean, complete, and statistically sound for analysis.

---

### 2. **Project Report**  
*Focus: Technical workflow and data engineering steps*

- **Integrated two raw datasets**:
  - `Unemployment in India.csv`
  - `Unemployment_Rate_upto_11_2020.csv`
- Performed **data cleaning**:
  - Removed nulls, dropped irrelevant columns (`longitude`, `latitude`)
- **Standardized structure**:
  - Unified column names and data types
  - Set all `Frequency` values to `'M'` (Monthly)
- **Merged datasets** using `pd.concat()` to create a single longitudinal dataset
- Exported final result as **`Full Data Unemployment Rate in India.csv`**

🔧 **Tools Used**: Pandas, NumPy  
🎯 **Outcome**: A robust, analysis-ready dataset spanning 2019–2020.

---

### 3. **Business Report**  
*Focus: Insights, trends, and analytical readiness*

- The merged dataset enables **multi-dimensional analysis**:
  - **Temporal trends**: Monthly unemployment changes (including pandemic impact in early 2020)
  - **Regional disparities**: Comparison across states (e.g., Andhra Pradesh most represented)
  - **Labor market dynamics**: Correlation between employment, unemployment, and participation rates
- Key findings:
  - **South** is the most frequently reported area (419 records)
  - Highest data density around **Feb–Mar 2020**—critical period for economic disruption
  - Data supports **time-series forecasting**, **regional benchmarking**, and **policy evaluation**
- Ready for advanced use cases:
  - Interactive dashboards (Plotly, Dash)
  - Predictive modeling (XGBoost, LightGBM)
  - Statistical testing (Mann-Whitney U, chi-square)

💡 **Strategic Value**: Enables evidence-based labor policy, economic monitoring, and crisis response planning.

---

## 🚀 Getting Started

1. Clone this repository  
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn plotly scikit-learn
   ```
3. Explore the notebooks in `/notebooks`  
4. Review the three reports in `/reports`

---

## 📌 Final Output

✅ **`Full Data Unemployment Rate in India.csv`**  
- 1,007 clean records  
- 7 standardized columns  
- Ready for visualization, modeling, and reporting

---

*This project is licensed under the MIT License.*
