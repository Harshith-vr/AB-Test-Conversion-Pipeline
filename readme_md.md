# AB-Test-Conversion-Pipeline

## 📌 Executive Summary
This project evaluates the performance of a new checkout user interface (UI) through a rigorous A/B testing pipeline. Using **DuckDB (SQL)** for data wrangling and **Python** for statistical analysis, this pipeline cleans raw session logs, mathematically validates the experimental design, and tests for statistical significance.

**Business Recommendation:** **DO NOT LAUNCH.** The new UI workflow did not produce a statistically significant improvement in conversion rates. The observed difference is due to statistical noise, and retaining the existing control page will prevent unnecessary engineering costs.

---

## 🛠️ Tech Stack & Methodology
* **Data Extraction & Cleaning:** SQL (`DuckDB`)
* **Statistical Analysis:** Python (`scipy.stats`, `statsmodels`)
* **Data Visualization:** Python (`matplotlib`, `seaborn`)

### Pipeline Workflow
1. **Data Wrangling (SQL):** Extracted 290,000+ raw user logs. Utilized Common Table Expressions (CTEs) and the `ROW_NUMBER()` window function to remove duplicate sessions and filter out corrupted routing data (users exposed to the wrong landing page).
2. **Experiment Validation (SRM Check):** Conducted a Chi-Square Goodness of Fit test to check for a Sample Ratio Mismatch (SRM). Validated that the 50/50 traffic split was healthy (p-value > 0.05), proving the routing algorithm functioned correctly.
3. **Hypothesis Testing (Z-Test):** Performed a two-proportion Z-test on the cleaned data to evaluate if the difference in conversion rates was statistically significant at a 95% confidence level ($\alpha = 0.05$).

---

## 📊 Results & Analysis

* **Control Group (Old Page):** 12.04% Conversion Rate
* **Treatment Group (New Page):** 11.88% Conversion Rate

The Z-test yielded a p-value greater than the 0.05 threshold. Therefore, we fail to reject the null hypothesis. The slight decrease in the treatment group's performance is not statistically significant, meaning the new design had no meaningful impact on user behavior.

---

## 🚀 How to Run the Project Locally

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/AB-Test-Conversion-Pipeline.git
   ```
2. Navigate to the project directory:
   ```bash
   cd AB-Test-Conversion-Pipeline
   ```
3. Install the required Python packages:
   ```bash
   pip install pandas duckdb scipy statsmodels matplotlib seaborn
   ```
4. Ensure the `ab_data.csv` dataset is in the same directory.
5. Run the Jupyter Notebook (`AB_Test_Conversion_Pipeline.ipynb`) or the Python script to execute the pipeline end-to-end.