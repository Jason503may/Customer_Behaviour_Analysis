# 🛍️ Customer Shopping Behavior Analysis

An end-to-end data analytics project that analyzes **3,900 customer purchase transactions** across multiple product categories to uncover spending patterns, customer segments, product preferences, and subscription behavior, with the goal of supporting strategic business decisions.

The project combines **Python (Jupyter Notebook)** for data preparation, **SQL (PostgreSQL)** for business analysis, and **Power BI** for interactive dashboarding.

---

## 📌 Table of Contents

- [Business Problem](#-business-problem)
- [Dataset](#-dataset)
- [Tools & Technologies](#-tools--technologies)
- [Project Workflow](#-project-workflow)
- [SQL Business Questions](#-sql-business-questions)
- [Power BI Dashboard](#-power-bi-dashboard)
- [Repository Structure](#-repository-structure)
- [How to Run](#-how-to-run)
- [Key Insights & Recommendations](#-key-insights--recommendations)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

---

## 🎯 Business Problem

A retail business wants to understand **how its customers shop** so it can make better decisions on marketing, pricing, discounts, subscriptions, and product strategy. This project answers questions such as:

- Who spends more: male or female customers? Which age groups drive the most revenue?
- Do discounts attract high-value purchases or just reduce margins?
- Do subscribers spend more than non-subscribers?
- Which products are best rated, most purchased, and most heavily discounted?
- How loyal are customers, and are repeat buyers more likely to subscribe?
- Does shipping type (Standard vs. Express) affect spending?

Full problem framing is available in `Business Problem Document.pdf`.

---

## 📊 Dataset

- **Size:** 3,900 purchase transactions
- **Granularity:** one row per customer purchase
- **Fields used in the analysis (as referenced in the SQL queries):**

| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `age` / `age_group` | Customer age and the derived age bracket |
| `gender` | Customer gender |
| `item_purchased` | Product bought |
| `category` | Product category |
| `purchase_amount` | Transaction value |
| `review_rating` | Customer rating of the product |
| `discount_applied` | Whether a discount was used (Yes/No) |
| `subscription_status` | Whether the customer is subscribed (Yes/No) |
| `shipping_type` | Shipping method (e.g., Standard, Express) |
| `previous_purchases` | Number of prior purchases (used for loyalty segmentation) |

> **Note:** the raw dataset file is not included in this repository. Add your CSV to the project folder before running the notebook (see [How to Run](#-how-to-run)).

---

## 🧰 Tools & Technologies

| Purpose | Tool |
|---|---|
| Data cleaning & preparation | Python, Pandas, Jupyter Notebook |
| Database & business analysis | PostgreSQL (SQL) |
| Visualization & reporting | Power BI |
| Documentation | PDF report & business problem document |

---

## 🔄 Project Workflow

1. **Define the business problem**: clarify the questions stakeholders need answered.
2. **Data preparation (Python):** load the dataset, inspect and clean it, and engineer helpful features such as `age_group`, in `Customer_Shopping_Behavior_Analysis.ipynb`.
3. **Load into PostgreSQL:** store the cleaned data in a `customer` table.
4. **SQL analysis:** answer 10 targeted business questions using aggregations, subqueries, CTEs, `CASE` logic, and window functions.
5. **Dashboard (Power BI):** visualize the findings in `customer_behavior_dashboard_01.pbix`.
6. **Report:** summarize insights and recommendations in `Customer Shopping Behavior Analysis.pdf`.

---

## 🧮 SQL Business Questions

All queries live in `customer_behavior_sql_queries.sql`.

| # | Business Question | SQL Concepts Used |
|---|---|---|
| 1 | Total revenue by male vs. female customers | `GROUP BY`, `SUM` |
| 2 | Customers who used a discount but still spent above the average purchase | Subquery, `AVG` |
| 3 | Top 5 products by average review rating | `AVG`, `ROUND`, `ORDER BY`, `LIMIT` |
| 4 | Average purchase amount: Standard vs. Express shipping | `WHERE ... IN`, `AVG` |
| 5 | Do subscribers spend more? (customers, avg spend, total revenue) | `COUNT`, `AVG`, `SUM` |
| 6 | Top 5 products with the highest share of discounted purchases | `CASE WHEN`, conditional aggregation |
| 7 | Segment customers into **New / Returning / Loyal** | CTE, `CASE WHEN` |
| 8 | Top 3 most purchased products within each category | CTE, `ROW_NUMBER() OVER (PARTITION BY ...)` |
| 9 | Are repeat buyers (>5 previous purchases) likely to subscribe? | Filtering, `GROUP BY` |
| 10 | Revenue contribution of each age group | `GROUP BY`, `SUM` |

**Customer segmentation logic (Q7):**

| Segment | Rule (based on `previous_purchases`) |
|---|---|
| New | = 1 |
| Returning | 2 – 10 |
| Loyal | > 10 |

---

## 📈 Power BI Dashboard

The file `customer_behavior_dashboard_01.pbix` contains an interactive dashboard that presents the key metrics and trends from the analysis (revenue, customer segments, product performance, subscription behavior, and more).

To view it, open the file in **Power BI Desktop** (Windows).

---

## 📁 Repository Structure

```
Customer_Behaviour_Analysis/
│
├── Business Problem Document.pdf              # Problem statement and objectives
├── Customer Shopping Behavior Analysis.pdf    # Final analysis report
├── Customer_Shopping_Behavior_Analysis.ipynb  # Python notebook: data prep & exploration
├── customer_behavior_sql_queries.sql          # 10 SQL business queries (PostgreSQL)
├── customer_behavior_dashboard_01.pbix        # Power BI dashboard
└── README.md
```

---

## ▶️ How to Run

### 1. Clone the repository
```bash
git clone https://github.com/Jason503may/Customer_Behaviour_Analysis.git
cd Customer_Behaviour_Analysis
```

### 2. Run the notebook
```bash
pip install pandas numpy jupyter
jupyter notebook Customer_Shopping_Behavior_Analysis.ipynb
```
Place the dataset CSV in the project folder and update the file path in the notebook if needed.

### 3. Run the SQL queries
1. Create a PostgreSQL database and load the cleaned data into a table named `customer`.
2. Open `customer_behavior_sql_queries.sql` in pgAdmin, DBeaver, or `psql` and run the queries.

### 4. Open the dashboard
Open `customer_behavior_dashboard_01.pbix` in Power BI Desktop.

---

## 💡 Key Insights & Recommendations

> Add the exact figures from your results here. The themes below follow directly from the questions the project answers.

- **Subscriptions:** compare average spend and revenue for subscribers vs. non-subscribers to decide whether to invest in subscription promotion.
- **Loyalty:** use the New / Returning / Loyal segmentation to design retention campaigns and reward programs.
- **Discounts:** identify heavily discounted products and check whether discounts are needed, or whether high spenders buy anyway.
- **Product strategy:** feature top-rated and top-selling products per category in marketing.
- **Shipping:** assess whether Express shipping customers spend meaningfully more than Standard customers.
- **Demographics:** target campaigns toward the age groups that contribute the most revenue.

---

## 🚀 Future Improvements

- Add RFM (Recency, Frequency, Monetary) analysis and customer clustering (K-Means).
- Build a churn or subscription-propensity prediction model.
- Include the sample dataset (or a data dictionary) in the repo for easy reproduction.
- Add a `requirements.txt` and dashboard screenshots to this README.

---

## 👤 Author

**Jason** ([@Jason503may](https://github.com/Jason503may))

If you found this project useful, consider giving it a ⭐!
