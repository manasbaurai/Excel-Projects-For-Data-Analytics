# 📊 Customer Churn Analysis — EDA Report

This report explores customer churn patterns from a telecom dataset. The goal is to understand **who is churning, why, and what factors drive it** — through exploratory data analysis and visualizations.

---

## 📁 Dataset Overview

The dataset ([Customer Churn.csv](Customer_Churn.csv)) contains customer demographic information, account details, and service subscriptions for a telecom company. Each row represents a customer, and the target variable is **Churn** (Yes/No).

**Key preprocessing steps performed:**
- Blank values in `TotalCharges` were replaced with `0` and the column was cast to `float`
- The `SeniorCitizen` column was encoded as binary integers (0/1) and converted to readable `Yes`/`No` labels
- No null values or duplicate rows were found after cleaning

---

## 🔍 Analysis & Visualizations

---

### 1. Churn Distribution (Count)

A bar chart showing the **raw count of churned vs. non-churned customers**. This gives an immediate sense of class imbalance — most customers have not churned, but the churned group is significant enough to analyze.

<img width="394" height="391" alt="image" src="https://github.com/user-attachments/assets/1810c0d4-660d-4b2c-8747-57149fc6229f" />

---

### 2. Churn Distribution (Percentage)

A pie chart showing the **percentage split between churned and retained customers**. This makes it easy to see the proportion at a glance — roughly 26–27% of customers have churned.

<img width="328" height="348" alt="image" src="https://github.com/user-attachments/assets/6d1a0ce2-fa85-4a51-8db7-b8cc691587c4" />

---

### 3. Churn by Gender

A grouped bar chart comparing churn counts across **Male and Female** customers. This helps determine whether gender is a significant factor in churn — the chart reveals that churn rates are nearly equal between genders, suggesting gender alone is not a strong predictor.

<img width="394" height="391" alt="image" src="https://github.com/user-attachments/assets/bd98a9c4-5b80-4758-94a7-0287f1094dfd" />

---

### 4. Churn by Senior Citizen (Count)

A grouped bar chart showing churn counts for **Senior vs. Non-Senior** customers. Senior citizens appear to churn at a higher absolute rate relative to their population share, indicating age could be a meaningful churn driver.

<img width="394" height="391" alt="image" src="https://github.com/user-attachments/assets/27ccfcf3-2570-47ba-af79-d96855aa656f" />

---

### 5. Churn by Senior Citizen (Percentage — Stacked Bar)

A stacked bar chart showing the **percentage of churned vs. retained customers within each Senior Citizen group**. This normalised view confirms that senior citizens have a noticeably higher churn rate (~40%+) compared to non-seniors (~23%), making senior status a key risk factor.

<img width="590" height="390" alt="image" src="https://github.com/user-attachments/assets/8142826e-e3e2-4489-bd2f-516f08da6503" />

---

### 6. Tenure Distribution

A histogram showing how long customers have been with the company (in months). The distribution reveals two spikes — one at very low tenure (new customers who churn quickly) and one at high tenure (long-loyal customers) — suggesting that **early months are the highest churn risk window**.

<img width="695" height="525" alt="image" src="https://github.com/user-attachments/assets/821d6fcf-bb24-425a-b2f0-83a6bf803927" />

---

### 7. Churn by Contract Type

A grouped bar chart showing churn counts across **Month-to-Month, One Year, and Two Year** contract types. Month-to-month customers churn at dramatically higher rates, while customers on longer contracts are far more likely to stay — **contract type is one of the strongest churn predictors** in the dataset.

<img width="472" height="371" alt="image" src="https://github.com/user-attachments/assets/32547d18-c10c-406b-89af-6d468ed821dc" />

---

## 🧩 Additional Analysis (Services)

A 3×3 grid of bar charts was generated to explore churn patterns across **9 service-related columns**:

<img width="1480" height="1189" alt="image" src="https://github.com/user-attachments/assets/2ab97fba-e815-4325-a63e-4a0e4c3f6d60" />


| Service | Insight |
|---|---|
| `PhoneService` | Customers without phone service show lower churn |
| `MultipleLines` | Minimal difference in churn across line options |
| `InternetService` | Fiber optic users churn at significantly higher rates |
| `OnlineSecurity` | Customers without online security churn more |
| `OnlineBackup` | Similar pattern — lack of backup = higher churn |
| `DeviceProtection` | Customers without protection churn more |
| `TechSupport` | No tech support strongly associated with churn |
| `StreamingTV` | Streaming users are split — contract type likely mediates this |
| `StreamingMovies` | Similar to StreamingTV |

---

## 📌 Key Takeaways

| Factor | Churn Risk |
|---|---|
| Month-to-month contract | 🔴 Very High |
| Senior citizen | 🟠 High |
| Short tenure (< 6 months) | 🟠 High |
| No online security / tech support | 🟠 High |
| Fiber optic internet | 🟡 Moderate |
| Gender | 🟢 Low (negligible difference) |

> **Conclusion:** Churn is most strongly driven by **contract type**, **tenure**, and **service add-ons**. Targeting month-to-month customers with retention offers — especially in their first few months — could significantly reduce overall churn.
