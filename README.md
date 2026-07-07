# Retail-demand-forecasting-Inventory-optimization
# Day 1- Phase-1
Download the Dataset from Kaggle and start understanding the data and project roadmap. Make a new desktop folder and sub-folders for save different files like notebook, sql, documents etc... https://www.kaggle.com/competitions/m5-forecasting-accuracy/data

---

## Project Overview

Retail Demand Forecasting & Inventory Optimization is a data analytics and forecasting project based on the Walmart M5 Forecasting dataset. The objective is to analyze historical sales patterns, pricing information, seasonal events, and product hierarchies to forecast future product demand and support inventory optimization decisions.

**Tools & Technologies:** Python, Pandas, NumPy, SQL, PostgreSQL, Power BI, Prophet, ARIMA, LightGBM

## Day 1 - Data Understanding

### Tasks Completed

- Created project folder structure.
- Organized dataset into the `data/raw` directory.
- Loaded all M5 Forecasting dataset files:
  - calendar.csv
  - sales_train_validation.csv
  - sell_prices.csv
  - sample_submission.csv
  - sales_train_evaluation.csv
- Performed initial dataset exploration.
- Checked dataset shapes, columns, and data types.
- Identified key datasets required for forecasting.
- Explored product hierarchy structure using Category and Department information.

### Key Findings

#### Calendar Dataset
- 1,969 rows and 14 columns.
- Contains date, event, SNAP program, and calendar-related information.
- Event-related null values are expected because events occur only on specific dates.

#### Sales Dataset
- 30,490 products.
- 1,913 days of historical sales data.
- Stored in wide format (`d_1` to `d_1913`).

#### Sell Prices Dataset
- Over 6.8 million records.
- Contains weekly product pricing information by store.

#### Product Hierarchy Identified

Category → Department

- HOBBIES
  - HOBBIES_1
  - HOBBIES_2
- HOUSEHOLD
  - HOUSEHOLD_1
  - HOUSEHOLD_2
- FOODS
  - FOODS_1
  - FOODS_2
  - FOODS_3

The M5 dataset consists of five files: calendar, sales, sell prices, sample submission, and evaluation data. The sales dataset contains 30,490 products with daily sales records across 1,913 days. The data follows a hierarchical structure from state → store → category → department → item, making it suitable for retail demand forecasting and inventory optimization. The calendar dataset provides event and seasonal information, while the sell prices dataset enables price-based demand analysis.
