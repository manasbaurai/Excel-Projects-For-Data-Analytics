# 🎬 Movies Dataset — Correlation Analysis Report

This report explores a movies dataset to uncover **correlations between various movie attributes** — including budget, gross revenue, votes, score, runtime, and more. The analysis follows a structured EDA pipeline: data cleaning, type correction, visualisation, and statistical correlation.

---

## 📁 Dataset Overview

The dataset ([movies.csv](movies.csv)) contains information about thousands of movies including their name, genre, rating, release year, score, votes, director, writer, star, country, budget, gross revenue, production company, and runtime.

---

## 🧹 Data Cleaning & Preprocessing

Before analysis, several cleaning steps were applied to ensure data quality:

### Step 1 — Checking for Missing Data
Each column was checked for the percentage of missing values. Most columns had 0% missing data. Only two columns had meaningful gaps:
- **`budget`** — 28% missing → rows dropped
- **`gross`** — 2% missing → rows dropped

### Step 2 — Dropping NaN Values
Rows with missing `budget` or `gross` values were dropped using `dropna()`, since these are the two primary columns used in correlation analysis.

### Step 3 — Fixing Data Types
Both `budget` and `gross` columns were cast from `float64` to `int64` for cleaner numerical representation.

### Step 4 — Parsing the `released` Column
The `released` column was converted to a proper `datetime` format using `pd.to_datetime()`. A new column `correctyear` was extracted from it to capture the actual release year (distinct from the existing `year` column).

### Step 5 — Sorting by Gross Revenue
The dataset was sorted in descending order by `gross` to surface the highest-earning movies first.

### Step 6 — Removing Duplicate Company Entries
Duplicate values were dropped from the `company` column to avoid skewing company-level aggregations.

---

## 📊 Analysis & Visualizations

---

### 1. Scatter Plot — Budget vs. Gross Revenue

A basic scatter plot to **visually inspect whether higher budgets lead to higher gross revenue**. Each point represents one movie. The upward trend suggests a positive relationship — movies with larger budgets tend to earn more — though there is considerable spread, indicating budget alone doesn't guarantee box office success.

<img width="536" height="468" alt="image" src="https://github.com/user-attachments/assets/a265a08a-bdef-4494-a07a-3be799fdabc6" />

---

### 2. Regression Plot — Budget vs. Gross Revenue

A regression plot using Seaborn's `regplot` that adds a **linear regression line (blue) over the scatter points (red)**. The regression line makes the positive correlation more explicit and quantifies the trend. The confidence band around the line shows the uncertainty of the fit — wider at extremes, tighter in the middle where most data lies.

<img width="691" height="622" alt="image" src="https://github.com/user-attachments/assets/b7104dd4-62df-404f-99ab-799742ccc7d8" />

---

### 3. Correlation Heatmap — Numeric Columns Only

A heatmap built from `df.corr(numeric_only=True)`, showing **pairwise Pearson correlation coefficients** between the numeric columns: `year`, `score`, `votes`, `budget`, `gross`, and `runtime`.

Key findings:
- **Budget ↔ Gross: 0.74** — Strong positive correlation (the strongest pair)
- **Votes ↔ Gross: 0.61** — Moderately strong; popular movies earn more
- **Score ↔ Votes: 0.47** — Higher-rated movies tend to get more votes
- **Runtime ↔ Score: 0.41** — Longer movies tend to score slightly higher

<img width="581" height="484" alt="image" src="https://github.com/user-attachments/assets/f10f8a4b-e95d-4670-b1cb-39e2de95bb80" />

---

### 4. Correlation Heatmap — All Columns (After Encoding)

To include non-numeric columns in the correlation analysis, all categorical/object columns (`name`, `rating`, `genre`, `director`, `writer`, `star`, `company`, `country`) were **label-encoded as category codes**. This allows a much broader heatmap covering all 16 columns.

Key additional findings from the full heatmap:
- **Genre ↔ Budget: -0.37** — Certain genres (e.g. animation, action) attract higher budgets
- **Votes ↔ Gross** and **Budget ↔ Gross** remain the strongest real-world correlations
- Most categorical columns (director, writer, star, company) show weak correlations with revenue metrics, confirming that no single person or company dominates outcomes

<img width="1032" height="577" alt="image" src="https://github.com/user-attachments/assets/378755e9-9744-4b0d-8837-cefc59cd8497" />

---

## 🔗 Sorted Correlation Pairs

All column pairs were unstacked and sorted by correlation value to rank them from most negative to most positive. This gives a clean list of the strongest relationships in the dataset.

**Highest positive correlations (> 0.5, excluding self-correlations):**

| Column A | Column B | Correlation |
|----------|----------|-------------|
| `gross` | `budget` | **0.74** |
| `budget` | `gross` | **0.74** |
| `gross` | `votes` | **0.61** |
| `votes` | `gross` | **0.61** |

**Notable negative correlations:**

| Column A | Column B | Correlation |
|----------|----------|-------------|
| `genre` | `budget` | **-0.37** |
| `gross` | `genre` | **-0.24** |
| `company` | `budget` | **-0.20** |

---

## 📌 Key Takeaways

| Insight | Strength |
|---|---|
| Budget is the strongest predictor of gross revenue | 🔴 Strong (0.74) |
| Vote count correlates with gross revenue | 🟠 Moderate (0.61) |
| Audience score correlates with vote count | 🟡 Moderate (0.47) |
| Runtime has a mild relationship with score | 🟢 Weak-Moderate (0.41) |
| Genre influences budget allocation | 🟡 Negative (-0.37) |
| Director/Star/Writer have minimal revenue impact | 🟢 Very Weak |

> **Conclusion:** The most statistically significant finding is the **strong positive correlation between budget and gross revenue (0.74)**. Movies with higher production budgets generally earn more. Audience engagement (votes) is the second strongest signal. Categorical attributes like director, writer, or star show surprisingly weak correlations, suggesting that star power alone is not a reliable revenue predictor in this dataset.
