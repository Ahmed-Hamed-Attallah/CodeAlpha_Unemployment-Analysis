# **Data Quality Report**

**Report Date**: October 30, 2025  
**Dataset**: Indian Regional Employment & Unemployment Statistics  
**Total Records**: 1,007  
**Time Period Covered**: May 2019 – February 2020 (Monthly frequency)  

---

## **1. Overview**

This dataset contains monthly estimates of unemployment, employment, and labor participation rates across 28 Indian regions grouped into 5 geographical areas. All records are complete with no missing values or duplicate entries.

---

## **2. Schema & Structure**

| Column | Data Type | Description |
|--------|----------|-------------|
| Region | `object` | Name of the Indian state/union territory |
| Date | `object` | End-of-month date (e.g., "31-05-2019") |
| Frequency | `object` | Reporting frequency (all values = "M" for monthly) |
| Estimated Unemployment Rate (%) | `float64` | % of labor force unemployed |
| Estimated Employed | `float64` | Estimated number of employed individuals |
| Estimated Labour Participation Rate (%) | `float64` | % of working-age population in labor force |
| Area | `object` | Geographical zone (North, South, East, West, Northeast) |

✅ **Observation**: Schema is consistent and well-defined. All 7 columns are fully populated (100% non-null).

---

## **3. Completeness**

- **Missing Values**: **None** — all 1,007 rows have complete data across all 7 columns.
- **Duplicates**: **None detected** — each row appears unique.

✅ **Conclusion**: Data is **100% complete** with no gaps or redundancies.

---

## **4. Validity & Consistency**

### **a) Frequency Field**
- All 1,007 entries = `"M"` (Monthly).
- ✅ **Valid and consistent**.

### **b) Date Format**
- Stored as string in `DD-MM-YYYY` format (e.g., `"31-05-2019"`).
- Contains **18 unique dates**, all aligning with month-end dates from **May 2019 to February 2020**.
- Most frequent date: `"29-02-2020"` (79 occurrences) — likely reflects data collection for all regions on that date.
- ⚠️ **Recommendation**: Convert to `datetime` type for time-series analysis and validation.

### **c) Categorical Fields**
- **Region**: 28 unique values (matches number of Indian states/UTs in scope). Top region: *Andhra Pradesh* (38 records).
- **Area**: 5 zones (North, South, East, West, Northeast). Distribution:
  - South: 419 (41.6%)
  - Other zones less represented.
- ✅ **Categories are valid and logically grouped**.

### **d) Numeric Ranges**

| Metric | Min | Max | Plausibility Check |
|-------|-----|-----|---------------------|
| Unemployment Rate (%) | 0.00 | 76.74 | ❗ **High max (76.74%)** — extreme but *possible* in crisis or small regions. Requires contextual validation. |
| Employed | 49,420 | 59,433,760 | ✅ Reasonable (e.g., large states like UP/Maharashtra vs. small UTs). |
| Labour Participation Rate (%) | 13.33 | 72.57 | ✅ Plausible (India’s national LPR typically 40–50%; regional variation expected). |

⚠️ **Note**: Unemployment rate of **76.74%** is an outlier. While not impossible (e.g., post-pandemic shock in a small region), it warrants verification.

---

## **5. Distribution & Outliers**

### **Numeric Summary**
| Statistic | Unemployment Rate (%) | Employed | Labour Participation Rate (%) |
|----------|------------------------|--------|-------------------------------|
| Mean | 11.91% | 8.996M | 42.38% |
| Median | 8.89% | 5.543M | 40.88% |
| Std Dev | 10.74 | 10.21M | 8.05 |
| Skew | Right-skewed (mean > median) | Highly right-skewed | Mild right skew |

- **Unemployment Rate**: 
  - 75% of values ≤ 16.13%
  - Max (76.74%) is **>4.5 std devs** above mean → **extreme outlier**.
- **Employed**: 
  - Huge std dev (10.2M) vs. mean (9M) → high variability across regions (expected).
- **Labour Participation**: 
  - Tighter distribution; 95% of values likely between 26%–58%.

✅ **Overall**: Distributions reflect real-world heterogeneity across Indian states.

---

## **6. Recommendations**

1. **Convert `Date` to `datetime`**  
   → Enables proper time-series analysis and validation (e.g., `pd.to_datetime(df['Date'], format='%d-%m-%Y')`).

2. **Investigate Extreme Unemployment Value (76.74%)**  
   → Confirm if data entry error or genuine (e.g., check corresponding `Region` and `Date`).

3. **Validate Region-Area Mapping**  
   → Ensure all 28 regions are correctly assigned to 5 zones (e.g., is "Telangana" in South?).

4. **Consider Normalization for Cross-Region Comparison**  
   → Use rates (not absolute employed numbers) for fair comparisons.

5. **Document Data Source & Methodology**  
   → Clarify how estimates were derived (e.g., CMIE, NSSO, PLFS?).

---

## **7. Overall Data Quality Score**

| Dimension | Score (/5) | Notes |
|---------|----------|-------|
| Completeness | 5 | No missing/duplicate data |
| Validity | 4 | Date format needs parsing; outlier requires check |
| Consistency | 5 | Uniform frequency; logical categories |
| Accuracy | 4 | Plausible except one extreme value |
| **Overall** | **4.5 / 5** | **High-quality dataset, minor validation needed** |