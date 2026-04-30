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
├── images/                     ← exported plot screenshots      
│   ├── missing_values.png   
│   ├── rating_distribution.png   
│   ├── top_cuisines.png   
│   ├── rating_vs_delivery.png   
│   └── correlation_heatmap.png   
│     
├── notebooks/   
│   └── zomato_eda.ipynb        ← main analysis notebook   
│  
│  
└── README.md   
```

## Analysis Walkthrough

1. **Data Overview** — shape, dtypes, head(), info()
2. **Missing Values & Duplicates** — null counts, bar chart, decision to drop
3. **Summary Statistics** — numerical and categorical describe
4. **Top Cities** — most represented cities in the dataset
5. **Country-Level Analysis** — restaurant count and avg rating per country
6. **Top Restaurant Chains** — most frequent restaurant names
7. **Rating Distribution** — histogram + KDE, filtered for rated restaurants only
8. **Votes Distribution** — skewness of the long-tail vote distribution
9. **Price Range Analysis** — distribution + avg rating by price tier
10. **Online Delivery Impact** — delivery availability vs average rating
11. **Table Booking vs Rating** — booking availability vs average rating
12. **Cuisine Analysis** — top 15 cuisines, avg rating per cuisine, cuisine vs delivery
13. **Correlation Heatmap** — numeric features: rating, votes, cost, price range

---

## Key Insights
 - **India dominates the dataset** — Around 90% of the restaurants are from India, even though the dataset is labeled as global.

 - **Most restaurants are unrated** — A significant number of restaurants have an Aggregate Rating of 0.0, likely representing newly listed or inactive restaurants.

 - **Ratings mostly cluster between 3.0 and 4.5** — The platform generally leans positive, with very few restaurants rated below 2.5 or above 4.8.

 - **Votes distribution is highly skewed** — A small fraction of restaurants receive the majority of customer votes, while most restaurants have very low engagement.

 - **North Indian and Chinese cuisines are the most common** — These cuisines dominate the dataset in terms of restaurant count.

 - **Rating vs Votes shows a moderate positive correlation (~0.4–0.5)** — Restaurants with higher engagement generally maintain better ratings, suggesting popularity and customer trust influence perception.

 - **Higher price ranges tend to have higher ratings** — Fine-dining and premium restaurants are generally rated better, though higher cost does not always guarantee quality.

 - **Average Cost for Two has little to no correlation with ratings** — Exact spending amount alone is not a reliable predictor of customer satisfaction.

 - **Table booking positively impacts ratings more than online delivery** — Restaurants offering table booking are more consistently associated with higher ratings.

 - **Online delivery is associated with slightly higher ratings** — Restaurants providing delivery services tend to perform better, especially in high-demand urban areas.

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
-  This EDA lays the groundwork for:
-  Rating prediction** — regression model using price range, votes, and cuisine as features
- [ ] Restaurant recommender** — content-based filtering on cuisine + location
- [ ] Geo-visualisation** — plotting restaurants on a world map using Folium
- [ ] Build a **rating prediction model** using the cleaned features (regression)
- [ ] Deploy findings as an interactive dashboard (Streamlit)
