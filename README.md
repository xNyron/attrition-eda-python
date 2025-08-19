https://github.com/xNyron/attrition-eda-python/releases

# Employee Attrition EDA with Python: Insights & Visuals Lab

[![Releases · Download](https://img.shields.io/badge/Releases-Download-blue?logo=github&style=for-the-badge)](https://github.com/xNyron/attrition-eda-python/releases)
[![Python](https://img.shields.io/badge/Python-3.8%2B-brightgreen)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-1.0%2B-4BC0C0)](https://pandas.pydata.org/)
[![matplotlib](https://img.shields.io/badge/matplotlib-3.0%2B-orange)](https://matplotlib.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

![Hero Image](https://images.unsplash.com/photo-1526378729146-85d6f48b9f20?auto=format&fit=crop&w=2000&q=80)

Table of contents
- About this repo
- Quick access (Download & run)
- What you will find
- Data overview
- Project structure
- Install and setup
- Run the analysis
- Notebook walkthrough
- Key EDA steps
- Visual examples
- How to read the plots
- Reuse and extend
- Automation and batch runs
- Performance tips
- Releasing and versioning
- Contributing
- License
- Contact and support
- Topics & keywords

About this repo
This repository holds a focused EDA project for employee attrition. The work uses Python, pandas, and matplotlib. It aims to show exit patterns and human resources signals. The code runs in Jupyter and as scripts. The visuals target HR teams and data analysts. The analysis highlights features that correlate with attrition. The notebooks document each step and show clear plots.

Quick access (Download & run)
- Go to the Releases page and download the asset. The release page contains packaged notebooks and scripts. Download the release file and execute it.
- Direct link to the release assets:
  https://github.com/xNyron/attrition-eda-python/releases
- Use the badge above for direct access to the same page.

What you will find
- Cleaned datasets used for EDA.
- Jupyter notebooks that walk through the analysis.
- One-click scripts to reproduce charts.
- Matplotlib figure exports in PNG and SVG.
- A small helper module for plot styling and common transforms.
- Sample dashboards exported as images.

Data overview
Dataset theme
- Employee demographic fields.
- Job role and level fields.
- Compensation and time-at-company.
- Performance ratings.
- Exit flag (Attrition: Yes/No).
- Dates: hire date and termination date.

Sample fields (common in HR attrition datasets)
- EmployeeID
- Age
- Gender
- MaritalStatus
- JobRole
- JobLevel
- Department
- MonthlyIncome
- YearsAtCompany
- YearsInCurrentRole
- YearsSinceLastPromotion
- PerformanceRating
- Attrition (Yes/No)
- OverTime (Yes/No)

Data quality notes
- We handle missing values via clear rules.
- We treat categorical codes as categories.
- We convert date columns to datetime type.
- We cap extreme numeric values for visual clarity.
- We avoid imputation that hides patterns.

Project structure
- README.md — this document
- data/
  - raw/ — raw datasets (kept read-only)
  - cleaned/ — cleaned CSVs used by notebooks
- notebooks/
  - 01_data_prep.ipynb
  - 02_univariate_analysis.ipynb
  - 03_bivariate_analysis.ipynb
  - 04_time_trends.ipynb
  - 05_model_ready_features.ipynb
- scripts/
  - run_eda.py — script to run the full EDA and export figures
  - export_figs.py — helper to render and save plots
- src/
  - utils.py — helper functions (load, plot style, transforms)
- outputs/
  - figures/ — generated PNG and SVG figures
  - reports/ — HTML export of notebooks

Install and setup
System prerequisites
- Linux, macOS, or Windows.
- Python 3.8 or later.
- At least 4 GB RAM for medium datasets.

Create a virtual environment
```bash
python -m venv .venv
source .venv/bin/activate    # macOS / Linux
.venv\Scripts\activate       # Windows
```

Install dependencies
```bash
pip install -r requirements.txt
```
Core dependencies
- pandas
- numpy
- matplotlib
- seaborn
- jupyter
- openpyxl (if you use Excel)
- scipy (optional)
The requirements.txt in the repo pins tested versions.

Run the analysis
From the repository root you can run the scripted flow. Download the release asset from the Releases page and run the main script. The release contains the same run_eda.py script and a packaged data folder. Download the release file and execute the main script.

Run from source
```bash
python scripts/run_eda.py --input data/cleaned/employee_attrition.csv --out outputs/figures
```
Run from release asset
- Download the release asset from:
  https://github.com/xNyron/attrition-eda-python/releases
- Extract the archive.
- Run the included run_eda.py file.
```bash
python run_eda.py --input employee_attrition_clean.csv --out ./figures
```

Notebook walkthrough
01_data_prep.ipynb
- Load raw data.
- Convert types.
- Impute selective missing values.
- Create derived features:
  - tenure_months
  - tenure_years (float)
  - promoted_last_5y (bool)
  - income_per_level (MonthlyIncome / JobLevel)

02_univariate_analysis.ipynb
- Inspect distributions.
- Plot histograms for numeric features.
- Show bar charts for categorical features.
- Flag skew, kurtosis, and outliers.

03_bivariate_analysis.ipynb
- Attrition vs numeric features using boxplots.
- Attrition vs categorical features using stacked bar charts.
- Correlation heatmap for numeric features.

04_time_trends.ipynb
- Attrition rate by year and quarter.
- Hire vs exit curves.
- Rolling averages of attrition.

05_model_ready_features.ipynb
- Encode categorical features.
- Create dummy features with controlled cardinality.
- Save model-ready CSV.

Key EDA steps
1. Load and inspect
- Use pandas to read CSV.
- Check head, info, and describe.
- Spot missing values and wrong types.

2. Clean and convert
- Convert categorical strings to category dtype.
- Parse dates into datetime.
- Rename fields for clarity.

3. Derive features
- Tenure in months and years.
- Promotion recency.
- Compensation ratio to department median.

4. Univariate analysis
- Histogram and density plots.
- Bar charts for counts.
- Table of top categories.

5. Bivariate analysis
- Boxplots of income by attrition.
- Chi-square tests for categorical variables.
- Point-biserial correlation for binary vs numeric.

6. Multivariate checks
- Pairwise scatter for numeric subset.
- Correlation matrix and heatmap.
- Conditional plots: attrition by job role and level.

7. Time series checks
- Attrition rate by month.
- Seasonal patterns by quarter.
- Hire and exit series comparison.

8. Export
- Save cleaned CSV.
- Export all figures as PNG and SVG.
- Save notebook as HTML.

Visual examples
This section shows typical figures and the code to make them. Each plot aims for clarity and reproducibility.

Histograms with KDE
```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data/cleaned/employee_attrition.csv')
plt.style.use('seaborn-whitegrid')
fig, ax = plt.subplots(figsize=(8,4))
df['MonthlyIncome'].plot(kind='hist', bins=40, density=True, alpha=0.6, ax=ax)
df['MonthlyIncome'].plot(kind='kde', ax=ax)
ax.set_title('Monthly Income Distribution')
ax.set_xlabel('Monthly Income (USD)')
plt.savefig('outputs/figures/monthly_income_hist.png', dpi=150)
```

Attrition rate by job role (stacked bar)
```python
role_table = pd.crosstab(df['JobRole'], df['Attrition'], normalize='index') * 100
role_table.sort_values('Yes', ascending=False, inplace=True)
role_table[['Yes','No']].plot(kind='bar', stacked=True, figsize=(10,6), color=['#d9534f','#5bc0de'])
plt.ylabel('Percent')
plt.title('Attrition Rate by Job Role')
plt.tight_layout()
plt.savefig('outputs/figures/attrition_by_role.png', dpi=150)
```

Correlation heatmap
```python
import seaborn as sns
num_cols = ['Age','MonthlyIncome','YearsAtCompany','YearsInCurrentRole','YearsSinceLastPromotion']
corr = df[num_cols].corr()
plt.figure(figsize=(6,5))
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt='.2f')
plt.title('Numeric Feature Correlation')
plt.savefig('outputs/figures/corr_heatmap.png', dpi=150)
```

Time series: Attrition rate by quarter
```python
df['ExitDate'] = pd.to_datetime(df['ExitDate'], errors='coerce')
df['Quarter'] = df['ExitDate'].dt.to_period('Q')
quarter_rate = df[df['Attrition']=='Yes'].groupby('Quarter').size() / df.groupby('Quarter').size()
quarter_rate = quarter_rate.fillna(0)
quarter_rate.plot(figsize=(10,4), marker='o')
plt.title('Quarterly Attrition Rate')
plt.ylabel('Attrition Rate')
plt.xlabel('Quarter')
plt.grid(True)
plt.savefig('outputs/figures/quarterly_attrition_rate.png', dpi=150)
```

How to read the plots
- Histogram: See shape and skew. A right skew may mean a few high earners.
- KDE: Smooth view of distribution.
- Boxplot by attrition: Compare medians and IQR. Large difference suggests a strong signal.
- Stacked bar: Shows percent of attrition vs stayers by category.
- Correlation heatmap: Values near 1 or -1 show strong linear correlation.
- Time series: Look for trends and seasonality.

Interpretation guide (practical)
- If attrition peaks for low job levels, the issue may be career path.
- High overtime with high attrition suggests workload risk.
- Low income with high attrition in same role suggests pay inequity.
- Sudden spikes in a quarter point to events. Investigate HR events in that period.

Feature engineering ideas
- Tenure bucket (0-1, 1-3, 3-5, 5+ years).
- Income percentile within department.
- Promotion gap (years since last promotion > 3).
- Composite stress index: overtime + years in current role + low performance.

Automated checks and tests
- Unit test for loaders: shape and column types.
- Validation test: attrition column % within expected range.
- Range checks: monthly income non-negative and within reasonable max.

Reproducible exports
- Save figure with fixed DPI and vector output for SVG.
- Use consistent theme via matplotlib.rcParams.
- Keep raw data separate from cleaned data.

Automation and batch runs
- The release includes run_eda.py to export all figures.
- The script accepts input and output paths and a profile flag.
- Use cron or CI to regenerate reports monthly.

Sample run_eda.py flags
```
usage: run_eda.py [-h] --input INPUT --out OUT [--profile PROFILE]

--input   Path to cleaned CSV
--out     Path to output directory
--profile Which subset to run: full, quick, demo
```
- full: runs all notebooks and exports everything.
- quick: runs a subset of plots for fast iteration.
- demo: a small sample dataset for quick demos.

Performance tips
- Use dtype specification in read_csv for large files.
- Use chunked reads for very large datasets.
- Sample for plotting when records exceed 200k.
- Cache intermediate transforms in parquet.

Releasing and versioning
- Tag releases with semantic versioning.
- Attach packaged data and script assets to each release.
- The Releases page holds artifacts. Download the release asset file and run the included script.

Releases and download
- Release files contain packaged notebooks and scripts.
- Download the release file and execute the script named run_eda.py that is included.
- Visit:
  https://github.com/xNyron/attrition-eda-python/releases
- Use the badge at the top to open the same page.

Figures and examples (embedded)
- Histogram example:
  ![Histogram Example](https://raw.githubusercontent.com/mwaskom/seaborn-data/master/README.md)
- Correlation example:
  ![Heatmap Example](https://upload.wikimedia.org/wikipedia/commons/1/18/Heatmap.png)
- Stacked bar example:
  ![Bar Example](https://images.unsplash.com/photo-1556157382-97eda2d62296?auto=format&fit=crop&w=1200&q=80)

Note: The images above illustrate chart types. The repo exports figures for each analysis step.

Reuse and extend
- Replace the input CSV with your HR data. Keep column names consistent or update the loader.
- Add new notebooks for churn modeling or survival analysis.
- Swap matplotlib with plotly if you need interactivity.

Common extensions
- Survival analysis with lifelines.
- Time-to-event modeling.
- Clustering of exit patterns.
- Text analysis of exit interviews.

Code style and utility functions
- The src/utils.py contains loader functions.
- Use utils.load_data(path) to get a cleaned DataFrame.
- Use utils.plot_style() to apply a consistent style.

Sample loader
```python
def load_data(path):
    df = pd.read_csv(path, parse_dates=['HireDate','ExitDate'], dtype={'EmployeeID':str})
    df['Attrition'] = df['Attrition'].astype('category')
    return df
```

Testing and CI
- Add a small test dataset in tests/ for CI runs.
- Use GitHub Actions to run the quick profile nightly.
- Save artifacts (figures and HTML) on CI for review.

Contributing
- Fork the repo.
- Create a branch per feature.
- Add tests for new loaders and plots.
- Open a PR with a clear description.

Issues
- Open issues for bugs and data questions.
- Label issues with "data", "notebook", or "script" for triage.
- Provide reproducible steps in issue text.

License
- The repository uses the MIT license.
- See LICENSE file for details.

Contact and support
- Open a GitHub issue for bugs or questions.
- Use PRs for code contributions.

Topics & keywords
- attrition-insights-with-python
- data-analysis
- eda
- eda-employee-attrition-jupyter
- employee-exit-patterns-eda
- hr-attrition-data-analysis
- matplotlib
- matplotlib-figures
- matplotlib-pyplot
- python

Badges and links
- Use the Releases badge near the top to access release artifacts. The badge links to:
  https://github.com/xNyron/attrition-eda-python/releases
- The Releases page includes built artifacts. Download the release file and run the included script.

Appendix: Example checklist before run
- [ ] Clone repo or download release.
- [ ] Install dependencies.
- [ ] Place cleaned CSV in data/cleaned.
- [ ] Run the script or open notebooks.
- [ ] Export figures to outputs/figures.
- [ ] Review outputs/reports HTML exports.

Appendix: Minimal run commands
```bash
git clone https://github.com/xNyron/attrition-eda-python.git
cd attrition-eda-python
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python scripts/run_eda.py --input data/cleaned/employee_attrition.csv --out outputs/figures
```

Appendix: Example outputs to expect
- outputs/figures/monthly_income_hist.png
- outputs/figures/attrition_by_role.png
- outputs/figures/corr_heatmap.png
- outputs/reports/eda_report.html

Appendix: Quick tips for HR stakeholders
- Focus on role and level patterns, not just raw attrition rate.
- Compare attrition to hiring rates.
- Consider cohort analysis for new hires.
- Check for spikes after compensation cycles or reorgs.

Emoji legend
- 📈 Charts and time series.
- 🧭 Guidance and steps.
- 🛠️ Tools and scripts.
- 📦 Releases and downloads.
- 🧪 Tests and CI.

End of file