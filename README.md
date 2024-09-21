# Credit Card Financial Dashboard - Power BI

## Project Overview

This project focuses on creating a **Credit Card Financial Dashboard** using Power BI, providing real-time insights into key performance metrics and trends for credit card operations. The dashboard is updated on a weekly basis, offering stakeholders actionable data to monitor and analyze financial metrics efficiently.

## Project Objective

The goal is to develop a comprehensive dashboard that offers insights into various aspects of credit card usage, including revenue, transactions, customer demographics, and more. By integrating SQL and DAX for data manipulation and visualization, the dashboard helps in identifying trends and making data-driven decisions.

## Features

- **Revenue Analysis**: Tracks weekly revenue and compares current week vs previous week revenue.
- **Transaction Insights**: Analyzes total transaction amounts and counts to understand trends.
- **Customer Demographics**: Breaks down customer data by age and income groups.
- **Geographical Insights**: Highlights the contribution of different states (TX, NY, CA) to total transactions.
- **Credit Card Categories**: Identifies the most popular credit card types (Blue & Silver).
- **Performance Metrics**: Includes overall activation rates and delinquency rates.

## Data Source

The data used in this project comes from a SQL database, which contains credit card transaction and customer data. The data is processed and imported into Power BI for visualization.

## Technologies Used

- **SQL**: Used for data extraction and management.
- **Power BI**: For data visualization and dashboard creation.
- **DAX (Data Analysis Expressions)**: To create calculated columns and measures for analysis.

## SQL Setup

1. Prepare CSV files for credit card transaction and customer data.
2. Create necessary tables in your SQL database.
3. Import the CSV files into SQL using `INSERT` queries or your preferred data-loading method.

## DAX Formulas

Here are some key DAX queries used in the project:

- **Age Group Classification**:
    ```DAX
    AgeGroup = SWITCH(
        TRUE(),
        'public cust_detail'[customer_age] < 30, "20-30",
        'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
        'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
        'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
        'public cust_detail'[customer_age] >= 60, "60+",
        "unknown"
    )
    ```

- **Weekly Revenue Calculation**:
    ```DAX
    week_num2 = WEEKNUM('public cc_detail'[week_start_date])
    Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
    Current_week_Reveneue = CALCULATE(
        SUM('public cc_detail'[Revenue]),
        FILTER(
            ALL('public cc_detail'),
            'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
        )
    )
    ```

## Insights

### Weekly Report (Week 53 - 31st Dec)

- **Revenue**: Increased by **28.8%** compared to the previous week.
- **Transaction Volume**: Significant growth in transaction amount and count.
- **Customer Growth**: Customer count saw a notable increase.

### Year-To-Date (YTD) Overview:

- Total Revenue: **57M**
- Interest Earned: **8M**
- Transaction Amount: **46M**
- Customer Breakdown: **Male customers** contributed 31M, **Female customers** contributed 26M.
- **Credit Cards**: Blue and Silver credit cards account for **93%** of transactions.
- **Geography**: TX, NY, and CA contribute to **68%** of total transactions.
- **Activation Rate**: **57.5%**
- **Delinquency Rate**: **6.06%**

