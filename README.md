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

# DAY-1 : Phase 2- Retail Demand Forecasting & Inventory Optimization

This project focuses on forecasting retail product demand and supporting inventory optimization using the Walmart M5 Forecasting dataset. Historical sales, pricing information, calendar events, and seasonal patterns are analyzed to understand customer demand behavior and improve inventory planning decisions.

The project aims to build a data-driven forecasting pipeline that identifies demand trends across stores, categories, and departments. By leveraging time-series analysis and machine learning techniques, the solution helps reduce stockout risks, minimize excess inventory, and improve supply chain efficiency.

**Tools & Technologies:** Python, Pandas, NumPy, SQL, PostgreSQL, Power BI, Prophet, ARIMA, LightGBM, Matplotlib, Seaborn

## Phase 2 - Data Understanding & Business Understanding

### Objectives
- Understand the structure of the Walmart M5 Forecasting dataset.
- Identify datasets required for demand forecasting.
- Explore product hierarchy, store structure, and sales data characteristics.
- Assess data quality before starting the cleaning phase.

### Tasks Completed

#### Dataset Exploration
Loaded and analyzed the following datasets:

- calendar.csv
- sales_train_validation.csv
- sell_prices.csv
- sample_submission.csv
- sales_train_evaluation.csv

Dataset Shapes:

| Dataset | Rows | Columns |
|----------|--------:|---------:|
| Calendar | 1,969 | 14 |
| Sales Train Validation | 30,490 | 1,919 |
| Sell Prices | 6,841,121 | 4 |
| Sample Submission | 60,980 | 29 |
| Sales Evaluation | 30,490 | 1,947 |

#### Business Understanding

Identified the hierarchical structure used by Walmart:

State → Store → Category → Department → Product

Categories discovered:
- FOODS
- HOUSEHOLD
- HOBBIES

Departments discovered:
- FOODS_1
- FOODS_2
- FOODS_3
- HOBBIES_1
- HOBBIES_2
- HOUSEHOLD_1
- HOUSEHOLD_2

#### Store Analysis

Total States:
- CA (California)
- TX (Texas)
- WI (Wisconsin)

Total Stores:
- 10 Stores

Store IDs:
- CA_1, CA_2, CA_3, CA_4
- TX_1, TX_2, TX_3
- WI_1, WI_2, WI_3

#### Product Analysis

- Total Unique Products: 3,049
- Total Product-Store Combinations: 30,490
- Total Historical Sales Days: 1,913

Category Distribution:

- FOODS: 14,370
- HOUSEHOLD: 10,470
- HOBBIES: 5,650

#### Calendar Analysis

Historical date range:

29-Jan-2011 to 19-Jun-2016

Event-related columns contain missing values because events occur only on selected dates. These missing values represent the absence of events rather than data quality issues.

#### Sales Statistics

Initial statistical analysis revealed:

- No missing values in sales records.
- Large number of zero-sales observations.
- Significant variation between products.
- Presence of intermittent demand patterns, which is common in retail forecasting datasets.

### Key Findings

- Main forecasting dataset identified: `sales_train_validation.csv`
- Supporting datasets: `calendar.csv` and `sell_prices.csv`
- Competition-specific datasets (`sample_submission.csv` and `sales_train_evaluation.csv`) are not required for the portfolio project.
- Data follows a hierarchical retail structure suitable for demand forecasting and inventory optimization.
- Dataset contains over five years of historical sales data, making it suitable for time-series forecasting.

---

# DAY :- 2
## Phase 3 - Data Cleaning & Data Quality Checks

Completed the initial data cleaning phase of the Retail Demand Forecasting & Inventory Optimization project. Converted date fields into proper datetime format for future time-series analysis and forecasting. Performed detailed memory usage analysis across all datasets and optimized categorical columns to improve processing efficiency.

A major optimization was achieved in the sell_prices dataset, reducing memory consumption from approximately 853 MB to 124 MB by converting repetitive string columns into categorical datatypes. Missing values were analyzed and validated as expected business-driven nulls related to event information. Duplicate record checks were performed on all datasets, and no duplicate records were found.

The datasets are now cleaned, validated, and ready for preprocessing, transformation, and dataset integration steps required for forecasting and inventory optimization.

### Data Cleaning Summary

## Tasks Completed

- Reloaded all required datasets.
- Converted date column to datetime format.
- Checked dataset memory usage.
- Performed memory optimization using categorical datatypes.
- Reduced sell_prices dataset memory from 853 MB to 124 MB.
- Verified data types across all datasets.
- Assessed missing values in calendar event columns.
- Confirmed that event-related null values represent non-event days.
- Performed duplicate record checks.
- No duplicate records were found in any dataset.

## Key Outcomes

- Date column successfully converted for time-series analysis.
- Significant memory reduction achieved in the prices dataset.
- Data quality checks completed.
- No duplicate records detected.
- Dataset is now ready for preprocessing and transformation.

---

# Day 3- PHASE- 4:- Data Preprocessing

### Data Preprocessing & Feature Integration – FOODS_1 Department

Today, the preprocessing pipeline for the FOODS_1 department was successfully completed. The objective was to transform raw retail sales data into a forecasting-ready time series dataset suitable for demand forecasting and inventory optimization.

The sales dataset was first filtered to include only the FOODS_1 department. Since the original sales data was stored in a wide format with daily sales spread across thousands of columns (d_1 to d_1913), it was converted into a long-format structure using the pd.melt() function. This transformation produced a time-series friendly dataset containing over 4.1 million records.

The transformed sales data was then merged with the calendar dataset to map each day identifier (d) to its actual date and corresponding retail week (wm_yr_wk). This step enabled proper temporal analysis and future forecasting activities.

Next, the pricing dataset was integrated using a composite key consisting of store_id, item_id, and wm_yr_wk. This allowed historical selling prices to be attached to each sales transaction. During validation, approximately 14.55% of price values were found to be missing. Further investigation confirmed that these missing values were caused by unavailable historical pricing records in the source dataset rather than merge errors.

A complete quality assessment was performed, including dataset shape validation, memory usage inspection, descriptive statistics, and missing value analysis. The final processed dataset contained sales, calendar, and pricing information in a unified structure.

### Final Processed Dataset
- Department: FOODS_1
- Rows: 4,132,080
- Columns: 11
- File Size: ~366 MB
- Missing Sales Values: 0
- Missing Price Values: 601,342 (14.55%)

### Key Learning

This phase demonstrated how large-scale retail data can be transformed from a transactional format into a forecasting-ready dataset while preserving business-critical information such as pricing and calendar effects. The validated preprocessing pipeline will now be reused for the remaining retail departments to build a complete forecasting dataset.
