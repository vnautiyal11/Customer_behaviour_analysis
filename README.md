# 📊 Customer Behaviour Analysis

## 📌 Overview
This project focuses on analyzing customer purchasing behavior using structured data stored in PostgreSQL. The objective is to extract meaningful insights about customer patterns, product performance, and business strategies using SQL-based analytics.

The analysis includes revenue trends, customer segmentation, product insights, and behavioral comparisons to support data-driven decision-making.

---

## 🎯 Objectives
- Understand customer purchasing patterns
- Identify high-performing products
- Analyze the impact of discounts and subscriptions
- Segment customers based on behavior
- Evaluate revenue contribution across demographics

---

## 🛠️ Tech Stack
- **Database**: PostgreSQL  
- **Query Language**: SQL  
- **Tools**: pgAdmin / Jupyter Notebook  
- **Data Processing**: CSV → PostgreSQL  

---

## 📂 Dataset
- File: `cleaned_data.csv`
- Contains customer transaction data including:
  - Customer demographics (age, gender)
  - Purchase details (amount, product, category)
  - Behavioral data (previous purchases, subscription status)
  - Shipping and discount information
  - Product reviews

---

## 🗄️ Database Schema

**Database Name:** `customer_db`  
**Table Name:** `customer_behavior`

Example columns:
- `customer_id`
- `age`
- `gender`
- `item_purchased`
- `category`
- `purchase_amount`
- `review_rating`
- `shipping_type`
- `discount_applied`
- `subscription_status`
- `previous_purchases`
- `age_group`

---

## 🔍 Key Analysis Queries

### 1. Revenue by Gender
```sql
SELECT gender, SUM(purchase_amount) AS revenue
FROM customer_behavior
GROUP BY gender;
2. Discount Impact Analysis
SELECT customer_id, purchase_amount 
FROM customer_behavior 
WHERE discount_applied = 'Yes'
AND purchase_amount >= (
    SELECT AVG(purchase_amount) FROM customer_behavior
);
3. Top Rated Products
SELECT item_purchased, ROUND(AVG(review_rating::numeric),2)
FROM customer_behavior
GROUP BY item_purchased
ORDER BY AVG(review_rating) DESC
LIMIT 5;
4. Shipping Type Comparison
SELECT shipping_type, ROUND(AVG(purchase_amount),2)
FROM customer_behavior
GROUP BY shipping_type;
5. Subscription Impact
SELECT subscription_status,
       COUNT(*) AS customers,
       AVG(purchase_amount) AS avg_spend,
       SUM(purchase_amount) AS total_revenue
FROM customer_behavior
GROUP BY subscription_status;
6. Customer Segmentation
New: 1 purchase
Returning: 2–10 purchases
Loyal: >10 purchases
```
📊 Key Insights
Identifies spending patterns across demographics
Highlights effectiveness of discounts
Reveals top-performing products and categories
Helps understand customer loyalty and retention
Supports targeted marketing strategies
🚀 How to Run
1. Load Data into PostgreSQL
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine("postgresql://postgres:password@localhost:5432/customer_db")

df = pd.read_csv("cleaned_data.csv")
df.to_sql("customer_behavior", engine, if_exists="replace", index=False)
2. Run SQL Queries
Use pgAdmin or any SQL client
Execute queries from the analysis section
📈 Future Enhancements
Integrate Power BI dashboard
Add machine learning for prediction
Perform customer segmentation using clustering
Build recommendation system
