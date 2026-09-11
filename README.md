# 🍽️ Zomato Data Analytics – SQL & Power BI Based Business Intelligence Platform



## 📘 Project Description

This project simulates a real-time food delivery analytics system using **PostgreSQL** and **Power BI**. By emulating Zomato’s operational environment, we created a full-stack data pipeline—from raw data preprocessing to advanced query analytics and KPI visualization.

The objective was to derive actionable insights into:
- Restaurant performance  
- User behavior patterns  
- Cuisine popularity  
- Sales trends across time and geography  

---

## 🛠️ Tech Stack & Tools

| Category               | Tools Used                          |
|------------------------|-------------------------------------|
| Database Engine        | PostgreSQL + pgAdmin4               |
| Data Visualization     | Microsoft Power BI                  |
| Data Processing        | Python + Pandas                     |
| Schema & Modeling      | Draw.io (ERD), SQL (DDL)            |
| SQL Concepts           | CTEs, Window Functions, Correlation |
| Data Import / Export   | Excel, Python-generated SQL         |

---

## 🔗 Key Links

- 📂 **GitHub Repository**: https://github.com/abizer007/Zomato_Analytics_Dashboard/tree/main
- 📊 **Live Power BI Dashboard**: https://abizer007.github.io/Zomato_Analytics_Dashboard/ 

---

## 🧱 Database Schema Overview

- **6 Core Tables**: `users`, `restaurants`, `orders`, `order_type`, `menu`, `food`
- **1 Normalized Bridge Table**: `menu_cuisine`
- Complies with **1NF, 2NF, 3NF**
- Supports **foreign keys**, **one-to-many**, and **composite relationships**

> 📎 ER Diagram:
>
> 
<img src="https://github.com/user-attachments/assets/c05327f2-a0b0-48ca-a66d-c65780dd44a1" width="400" height="500"/>


---

## 🖥️ PostgreSQL Server Setup & Execution Snapshots

To manage our backend database, we used **PostgreSQL** as the primary engine and **pgAdmin4** for GUI-based interaction. This section highlights the actual execution environment and setup used during development:

### 🔧 Server Configuration

- **Host**: `localhost`
- **Port**: `5432`
- **User**: `postgres`
- **Database Name**: `zomato_analytics`
- **Authentication**: Password-protected (secured with role-based privileges)

### 📁 Schema Execution in pgAdmin

#### 📌 pgAdmin4 Dashboard  
*This image displays the pgAdmin4 interface where all tables were created, queried, and verified.*

![image](https://github.com/user-attachments/assets/abd7201a-aebb-4121-8a9a-aa6c94aace9d)

#### 📌 Table Visualization  
*Visual representation of inserted rows in `restaurants`, `orders`, `users`, and `menu_cuisine`.*

![image](https://github.com/user-attachments/assets/1080c218-92ef-4b22-91e8-ae20c6a5a528)

#### 📌 Live Query Execution  
*Example of an advanced query using CTE and CORR() to analyze sales trend correlation.*

![image](https://github.com/user-attachments/assets/54fc83a2-fdde-4f97-8a51-676d71bbb712)


![image](https://github.com/user-attachments/assets/757541e3-d2a4-4bf2-ada4-89ad6758aec5)

---

## 🧮 Advanced SQL Query Highlights

- 🥇 Top-rated restaurants per city  
- 📆 Yearly + monthly + seasonal sales aggregation  
- 💡 Customer lifetime value & segmentation  
- 🍛 Most popular cuisines per geography  
- 📉 High-rated but underperforming restaurants  
- 📊 Sales trend correlation using `CORR()` over time  

> ✅ Full SQL query set

---

## 🧠 Power BI Dashboard Features

- 📌 Toggle between **Sales Amount** and **Order Quantity**
- 📍 Visualize **Top Performing Cities**
- 🧑‍🍳 Analyze **User behavior** by gender, age, and retention
- 🧾 Compare **Sales by Cuisine**, **Ratings vs Revenue**, and **Seasonal Variations**
- 🧭 Drill-downs for deep dives into city-level metrics

---

## 🖼️ Screenshots



### 1️⃣ Index Page  
![image](https://github.com/user-attachments/assets/80800781-8b28-4ebc-a84d-a1a46babe014)


### 2️⃣ Year-wise Sales & User Trends  
![image](https://github.com/user-attachments/assets/233f466b-7874-4ea6-b058-d57d867ea816)


### 3️⃣ User-Wise Performance & Ratings  
![image](https://github.com/user-attachments/assets/cbed04c3-cb22-4c54-a67c-c03ded75928b)


### 4️⃣ City Performance 
![image](https://github.com/user-attachments/assets/7bd89598-03a3-4f95-93d4-4e60e11dbf0f)


---

## ⚙️ Python Automation – Data Insertion

We used Python to generate SQL `INSERT` statements dynamically from Excel:

```python
import pandas as pd

# Load Excel file
df = pd.read_excel("restaurant.xlsx")

# Escape single quotes for SQL
def escape_sql(value):
    if pd.isna(value):
        return "NULL"
    value = str(value).replace("'", "''")
    return f"'{value}'"

# Table name
table_name = "restaurants"

# Create table SQL
create_table = f"""
CREATE TABLE {table_name} (
    id INTEGER PRIMARY KEY,
    name TEXT,
    country TEXT,
    city TEXT,
    rating TEXT,
    rating_count TEXT,
    cuisine TEXT,
    link TEXT,
    address TEXT
);
"""

# Insert rows
insert_lines = []
for _, row in df.iterrows():
    values = ", ".join(escape_sql(row[col]) for col in df.columns)
    insert_lines.append(f"INSERT INTO {table_name} VALUES ({values});")

# Save to file
with open("insert_restaurants.sql", "w", encoding="utf-8") as f:
    f.write(create_table + "\n" + "\n".join(insert_lines))

```

---

## 🧪 Learning Outcomes

- Built production-style **normalized relational schema**
- Applied **correlation, seasonal**, and **trend analysis** via SQL
- Learned **DAX**, **Power Query**, and custom **Power BI visuals**
- Gained experience in **ETL**, **data cleaning**, and **real-time reporting**

---

## ⚠️ Known Challenges & Solutions

| Issue                                | Solution |
|-------------------------------------|----------|
| PostgreSQL import performance       | Used PgAdmin4 & optimized batch inserts |
| Power BI slowness with big data     | Used **DirectQuery** and **aggregated imports** |
| 1NF Violation (Multi-cuisine)       | Created bridge table `menu_cuisine` |
| Missing & inconsistent entries      | Cleaned using Pandas & SQL filters |

---

## 📚 Recommended Use

This repository is ideal for:
- Students building **database-backed analytics systems**
- Analysts learning **SQL + Power BI integration**
- Academic demonstration of **data pipeline architecture**

---

🎥 **Power BI Reference Source**  
Our Power BI dashboard development was greatly guided by the following tutorial:  
[📺 Power BI Dashboard Tutorial for Beginners – by Learn with Whiteboard](https://youtu.be/if_ES7hC9Bc?si=ju2LM9YpdTG9zb7M)



> **“Data is only as powerful as the decisions it fuels.”**
