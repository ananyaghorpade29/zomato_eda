# 🍽️ Zomato Restaurant Data — Exploratory Data Analysis

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> **What makes a restaurant successful on Zomato?**  
> This project digs into 9,500+ global restaurant listings to uncover patterns in ratings, cuisines, pricing, delivery options, and geography — using end-to-end exploratory data analysis.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Analysis Walkthrough](#analysis-walkthrough)
- [Key Insights](#key-insights)
- [Tech Stack](#tech-stack)
- [How to Run](#how-to-run)
- [What I Learned](#what-i-learned)
- [Next Steps](#next-steps)

---

## Project Overview

This is my first end-to-end data analysis project. The goal was to move beyond toy examples and practice real-world EDA skills — handling messy data, making decisions about missing values, and communicating findings clearly through visualizations.

**Core questions explored:**
- How are restaurant ratings distributed globally?
- Which cuisines dominate the platform?
- Do online delivery and table booking affect ratings?
- Is there a relationship between price range and rating?
- Which cities and localities have the highest-rated restaurants?

---

## Dataset

| Property | Detail |
|---|---|
| Source | [Zomato Restaurants Dataset — Kaggle](https://www.kaggle.com/datasets/shrutimehta/zomato-restaurants-data) |
| Rows | 9,551 restaurants |
| Columns | 21 features |
| Geography | Global (15+ countries) |
| Key features | `Aggregate rating`, `Cuisines`, `Price range`, `Has Online delivery`, `Has Table booking`, `Votes`, `City`, `Locality` |

**Column overview:**

```
Restaurant ID, Restaurant Name, Country Code, City, Address,
Locality, Longitude, Latitude, Cuisines, Average Cost for two,
Currency, Has Table booking, Has Online delivery, Is delivering now,
Price range, Aggregate rating, Rating color, Rating text, Votes
```

---

## Project Structure

```
zomato-eda/
│
├── data/
│   └── zomato.csv              ← raw dataset (download from Kaggle)
│
├── notebooks/
│   └── zomato_eda.ipynb        ← main analysis notebook
│
├── images/                     ← exported plot screenshots
│   ├── missing_values.png
│   ├── rating_distribution.png
│   ├── top_cuisines.png
│   ├── rating_vs_delivery.png
│   └── correlation_heatmap.png
│
└── README.md
```

---

## Analysis Walkthrough

### 1. Data Loading & First Look
Loaded the dataset with `latin-1` encoding (required due to special characters in restaurant names). Confirmed shape of **9,551 rows × 21 columns** and reviewed data types.

### 2. Missing Value Analysis
Found missing values only in the `Cuisines` column — a very small proportion of the total dataset. Decision: **dropped null rows** since the count was negligible and imputation for cuisine names isn't meaningful.

```python
data.dropna(inplace=True)
# Result: 0 missing values, 0 duplicate rows
```

### 3. Summary Statistics
Computed `.describe()` for numerical columns. Key observations: rating ranges from 0 to 5, votes are heavily right-skewed, and price range is encoded as 1–4.

### 4. Univariate Analysis
- **Rating distribution:** Plotted with `sns.histplot` + KDE curve. Ratings cluster around **3.5–4.5** with very few restaurants below 2.5.
- **Top cuisines:** Bar chart of most frequent cuisine types across all restaurants.
- **Price range distribution:** Majority of restaurants fall in price range 1–2 (budget-friendly).

### 5. Bivariate Analysis
- **Rating vs Online Delivery:** Box plots comparing ratings for restaurants with/without online delivery.
- **Rating vs Table Booking:** Restaurants offering table booking tend to skew towards higher ratings.
- **Votes vs Rating:** Scatter plot showing moderate positive relationship.

### 6. Correlation Analysis
Built a correlation heatmap for numerical features: `Aggregate rating`, `Votes`, `Price range`, `Average Cost for two`.

```python
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f", linewidths=0.5)
```

---

## Key Insights

1. **Ratings cluster around 3.5–4.5** — the platform leans positive; very few restaurants fall below 2.5 or above 4.8.

2. **Rating vs Votes (~0.4–0.5 correlation)** — Moderate positive relationship. Restaurants with more engagement tend to maintain higher ratings, suggesting social proof matters.

3. **Price range vs Rating (~0.4 correlation)** — Higher price-tier restaurants score marginally better, but the effect is moderate — expensive doesn't guarantee excellent.

4. **Average Cost for Two ≈ no correlation** — Raw cost has almost no predictive value for ratings. It's the *price category* (1–4) that captures more signal than the exact number.

5. **Votes are heavily skewed** — A small number of restaurants receive the majority of votes. Most restaurants have very few reviews, which may inflate or deflate their ratings.

6. **Online delivery & table booking** — Restaurants offering these features tend to appear in slightly higher rating brackets, possibly because they serve higher-demand urban markets.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| `Python 3.11` | Core language |
| `Pandas` | Data loading, cleaning, and transformation |
| `Seaborn` | Statistical visualizations |
| `Matplotlib` | Plot customization and export |
| `Jupyter / VS Code .ipynb` | Interactive notebook environment |

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/ananyaghorpade29/zomato-eda.git
cd zomato-eda
```

**2. Install dependencies**
```bash
pip install pandas seaborn matplotlib jupyter
```

**3. Download the dataset**

Download `zomato.csv` from [Kaggle](https://www.kaggle.com/datasets/shrutimehta/zomato-restaurants-data) and place it in the `data/` folder.

**4. Open the notebook**
```bash
# In VS Code — open zomato_eda.ipynb directly
# Or via terminal:
jupyter notebook notebooks/zomato_eda.ipynb
```

---

## What I Learned

- How to handle encoding issues in real-world CSVs
- Making principled decisions about missing data (drop vs impute)
- The difference between *univariate* and *bivariate* analysis and when to use each
- How to read and communicate a correlation heatmap
- Structuring a notebook so that a non-technical reader can follow the story

---

## Next Steps

- [ ] Add geo-visualization (Folium map of restaurant density by country)
- [ ] Build a **rating prediction model** using the cleaned features (regression)
- [ ] Cuisine-level deep dive — which cuisines consistently rate highest?
- [ ] Deploy findings as an interactive dashboard (Streamlit)
