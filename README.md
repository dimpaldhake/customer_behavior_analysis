Customer Shopping Behavior Analysis

An end-to-end data analytics project that explores customer shopping patterns using Python, Pandas, PostgreSQL, SQL, and Power BI. The project prepares a customer shopping dataset, loads the cleaned data into PostgreSQL, answers business questions with SQL, and presents customer and revenue patterns in an interactive Power BI dashboard.

Project Overview

Retail businesses can use customer purchase data to understand who is buying, how much different groups spend, how discounts are used, and how shopping behavior varies by category and age group.

This project covers the following workflow:

Explore and inspect the raw dataset with Pandas.

Handle missing review ratings using the median rating within each product category.

standardize column names and create analysis-friendly fields.

Load the prepared DataFrame into a PostgreSQL table.

Run SQL queries to investigate customer segments, revenue, discounts, ratings, shipping, and purchasing patterns.

Visualize key measures in a Power BI dashboard.

Tools and Technologies

Python — data preparation and transformation

Pandas — data inspection, missing-value handling, and feature creation

Jupyter Notebook — analysis workflow

PostgreSQL — storing and querying the prepared dataset

SQL — business analysis, aggregation, subqueries, CTEs, CASE, and window functions

SQLAlchemy + psycopg2 — connecting Python to PostgreSQL

Power BI — dashboard and visual reporting

Dataset

The supplied CSV contains 3,900 records and 18 columns describing customer shopping behavior.

Main fields include:

Customer ID, age, gender, and location

Item purchased and product category

Purchase amount (USD), size, color, and season

Review rating

Subscription status

Shipping type

Discount applied and promo code used

Previous purchases

Payment method

Frequency of purchases

The CSV is the raw input dataset. The notebook transforms it before loading it into PostgreSQL.

Data Preparation

The Jupyter notebook (Customer_Shopping_Behavior_Analysis.ipynb) performs these steps:

Reads customer_shopping_behavior.csv into a Pandas DataFrame.

Inspects the dataset using head(), info(), describe(), and missing-value counts.

Fills missing Review Rating values with the median rating of the corresponding category.

Converts column names to lowercase and replaces spaces with underscores.

Renames purchase_amount_(usd) to purchase_amount.

Creates age_group using quartiles of the age column, labelled Young Adult, Adult, Middle-aged, and Senior.

Maps purchase frequency labels to an approximate number of days in purchase_frequency_days.

Drops promo_code_used after checking whether it matches discount_applied.

Loads the transformed DataFrame into PostgreSQL as the customer table using SQLAlchemy.

Important: The age-group labels are assigned using quartiles (pd.qcut), so they represent data-based age segments rather than fixed demographic age ranges.

SQL Analysis

The SQL file (customer_behavior_sql_queries.sql) contains 10 business questions:

Revenue by gender — compare total purchase revenue for male and female customers.

Discounted purchases above average — identify customers who used a discount and spent at least the average purchase amount.

Highest-rated products — find the five products with the highest average review rating.

Shipping comparison — compare average purchase amount for Standard and Express shipping.

Subscription and spending — compare customer count, average spend, and total revenue for subscribers and non-subscribers.

Discount rate by product — identify products with the highest percentage of purchases using discounts.

Customer segmentation — classify customers as New, Returning, or Loyal based on previous purchases.

Top products within each category — rank products by number of customer records within each category using ROW_NUMBER().

Repeat buyers and subscriptions — compare subscription status among customers with more than five previous purchases.

Revenue by age group — calculate and rank total revenue for each age group.

The SQL uses PostgreSQL syntax, including ::numeric, common table expressions (CTEs), conditional aggregation, subqueries, and window functions.

Power BI Dashboard

The Power BI report (customer_behavior_dashboard.pbix) contains visuals for:

Percentage of customers by subscription status

Revenue by category

Sales by category

Revenue by age group

Sales by age group

Slicers for exploring subsets of the data

The dashboard is intended to help compare customer groups and product categories and to explore revenue and sales patterns interactively.

Repository Structure

Keep the files together in your GitHub repository so the notebook can find the CSV using its relative filename:

customer-shopping-behavior-analysis/
├── customer_shopping_behavior.csv
├── Customer_Shopping_Behavior_Analysis.ipynb
├── customer_behavior_sql_queries.sql
├── customer_behavior_dashboard.pbix
└── README.md

How to Run the Analysis

1. Clone or download the repository

git clone <your-repository-url>
cd customer-shopping-behavior-analysis

2. Install the Python dependencies

Use a Python environment with Jupyter Notebook installed, then run:

pip install pandas sqlalchemy psycopg2-binary jupyter

3. Start Jupyter Notebook

jupyter notebook

Open Customer_Shopping_Behavior_Analysis.ipynb and run the cells in order. Keep the CSV in the same directory as the notebook.

4. Configure PostgreSQL

Create a PostgreSQL database named customer_behavior, then configure the database connection in the notebook using your own local credentials.

Security note: Do not commit database passwords or other secrets to GitHub. Read credentials from environment variables or a local configuration file excluded from version control. The notebook should not contain a real password.

The notebook writes the transformed DataFrame to a table named customer using if_exists="replace", which replaces that table when the loading cell is run again.

5. Run the SQL queries

Open customer_behavior_sql_queries.sql in a PostgreSQL client such as pgAdmin or psql, connect to the database containing the customer table, and run the queries.

6. Open the Power BI report

Open customer_behavior_dashboard.pbix in Power BI Desktop. If prompted, update the data source or refresh the data connection to match your own environment.

Skills Demonstrated

Data inspection and cleaning with Pandas

Missing-value treatment using group-level medians

Feature engineering and categorical grouping

Python-to-PostgreSQL data loading

SQL aggregations, filtering, subqueries, CTEs, CASE expressions, and window functions

Business-question translation and customer segmentation

Dashboard-based reporting with Power BI

Notes and Limitations

The supplied files show the analysis workflow and dashboard design; this README does not claim business findings or numerical conclusions that have not been verified from the report outputs.

The SQL assumes the transformed PostgreSQL table is named customer and includes fields such as purchase_amount and age_group.

The notebook currently contains a local database connection configuration. Replace hard-coded credentials with environment variables before publishing the notebook.

The SQL query for product rankings uses ROW_NUMBER(), so tied products receive different row numbers rather than sharing a rank.

Author

Dimpal Dhake

