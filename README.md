# 📊 Customer Dataset: Synthetic Data Generation & Data Quality Pipeline

## 🎯 Project Overview & Objective
In real-world data engineering and analytics projects, datasets are rarely clean. They often contain missing values, inconsistent text formats, extreme outliers, and duplicate records. 

The goal of this project is to simulate a realistic **Customer Churn & Behavioral Dataset** of 1,000 users, inject intentional data quality defects ("dirty data"), and demonstrate a complete data cleaning and Exploratory Data Analysis (EDA) pipeline using Python (`pandas`, `numpy`, `seaborn`).

---

## 📋 Data Dictionary (Dataset Content)

The dataset contains the following 8 key features designed to represent standard SaaS/E-commerce customer records:

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| **`Yas` (Age)** | Integer | Customer age (Standard range: 18–70). |
| **`Gelir` (Income)** | Float/Int | Estimated monthly customer income in local currency. |
| **`Sehir` (City)** | String | Customer location (e.g., İstanbul, Ankara, İzmir). |
| **`Abonelik_Tipi`** | String | Tiered service level (`Basic`: 50%, `Standard`: 30%, `Premium`: 20%). |
| **`Kayit_Tarihi`** | Datetime | Customer onboarding date (2022–2025 range). |
| **`Aylik_Harcama`** | Float | Average monthly spending amount. |
| **`Memnuniyet_Puani`**| Integer | Customer satisfaction rating on a scale from 1 to 5. |
| **`Churn`** | Binary (0/1)| Target variable indicating if the customer cancelled service (`1`) or stayed (`0`). |

---

## ⚠️ Why Inject "Dirty Data"? (The Engineering Rationale)

To test the robustness of our data processing pipeline, controlled anomalies were introduced into the raw dataset:

1. **Inconsistent Categorical Strings (`Sehir`):**
   * *Problem:* Variations like `"İstanbul"`, `"istanbul"`, `"İSTANBUL"`, and `" Antalya "` (with trailing spaces).
   * *Why:* Real users enter text differently across forms, leading to false unique categories during grouping.

2. **Missing Values (`NaN`):**
   * *Problem:* Randomly inserted missing entries in `Yas`, `Gelir`, and `Memnuniyet_Puani`.
   * *Why:* Simulates system logging failures, skipped optional survey fields, or corrupted data pipelines.

3. **Outliers & Extreme Values (`Gelir`):**
   * *Problem:* Injected disproportionately high income values (e.g., $2,000,000$).
   * *Why:* Demonstrates how extreme values distort statistical metrics (like the mean) and how boxplots help isolate them.

4. **Logical Anomalies (`Yas`):**
   * *Problem:* Negative ages (`-5`) and unrealistic values (`150`).
   * *Why:* Simulates form validation errors or bad user input.

5. **Duplicate Rows:**
   * *Problem:* Appended identical copied rows to the dataset.
   * *Why:* Mappings and API retries often create duplicate entries in real production databases.

---

## 🔬 Exploratory Data Analysis (EDA) & Insights

* **Distribution & Skewness Analysis:** Histograms combined with Kernel Density Estimation (KDE) help determine if financial metrics follow a normal or right-skewed distribution.
* **Outlier Isolation:** Boxplot visualization provides clear interquartile range (IQR) boundaries to identify extreme points without removing valid upper-tier income groups mistakenly.
* **Correlation Mapping:** Heatmaps quantify direct statistical relationships between numeric features (e.g., assessing whether higher monthly spend correlates with higher satisfaction or lower churn).
