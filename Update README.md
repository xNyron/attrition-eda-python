# 💼 Employee Attrition Analysis using Python

This project analyzes employee attrition using Python and Jupyter Notebook. The goal is to understand why employees leave the organization by identifying patterns and relationships between different features and attrition.

---

## 📊 Project Overview

**Attrition** refers to employees leaving the company. By analyzing employee data, we aim to uncover:
- Key factors that contribute to attrition
- Patterns in demographics, job satisfaction, and compensation
- Insights that can help reduce employee turnover

---

## 🧰 Tools Used

- **Python**
- **Jupyter Notebook**
- **Pandas** – for data manipulation and cleaning
- **Matplotlib** – for data visualization

---

## 📂 Dataset Overview

The dataset contains 30+ columns, including:

- **Demographics**: `Age`, `Gender`, `MaritalStatus`, `Education`
- **Job Info**: `JobRole`, `Department`, `MonthlyIncome`, `JobLevel`
- **Satisfaction Levels**: `JobSatisfaction`, `EnvironmentSatisfaction`, `WorkLifeBalance`
- **Performance Metrics**: `YearsAtCompany`, `OverTime`, `TrainingTimesLastYear`, etc.
- **Target Variable**: `Attrition` (Yes/No)

---

## 📌 Key Analyses Performed

### 🔹 Univariate Analysis
Explored individual features such as:
- Age distribution
- Count of attrition (Yes/No)
- Distribution of MonthlyIncome
- Frequency of different departments and roles

### 🔹 Bivariate Analysis
Compared features against attrition to find patterns:
- **Attrition vs Department**
- **Attrition vs Age Group**
- **Attrition vs MonthlyIncome**
- **Attrition vs JobSatisfaction**
- **Attrition vs WorkLifeBalance**

### 🔹 Feature Engineering
- Created custom `AgeGroup` buckets (e.g., 18–25, 26–35, etc.)
- Converted relevant columns to categorical types
- Dropped columns not useful for EDA like `EmployeeNumber`

---

## 📦 Files in this Repository

| File                      | Description                                      |
|---------------------------|--------------------------------------------------|
| `Attrition_PreprocessingData.ipynb`| Jupyter Notebook containing the full EDA process |
| `cleaned_data.csv`          | Cleaned dataset after preprocessing              |
| `README.md`               | Project explanation and documentation            |

---

## ✅ Key Findings

- Employees with **low job satisfaction** and **low monthly income** are more likely to leave.
- **Younger age groups** and **overtime workers** show higher attrition rates.
- Attrition is more common in some **departments** and **job roles** than others.
- **Work-life balance** and **years at company** also show important trends.

---

## 🚀 Future Work

- Perform multivariate analysis or correlation heatmaps
- Train a classification model to predict attrition (e.g., Logistic Regression)
- Create interactive dashboards using Streamlit or Dash

---

## 🧠 Conclusion

Through detailed EDA, this project identifies the most important factors associated with employee attrition. These insights can help HR teams develop strategies to improve employee satisfaction and reduce turnover.

