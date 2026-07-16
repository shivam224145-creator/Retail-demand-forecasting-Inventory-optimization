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

# Day 3- PHASE- 4:- Data Preprocessing[Part-1]

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

---

# Day 4- PHASE- 4:- Data Preprocessing[Part-2]

## Department-Wise Data Processing Pipeline Completion

### Department-Wise Data Processing Completed
- Created a reusable preprocessing function for all departments.
- Converted sales data from wide format to long format using pd.melt().
- Merged sales data with calendar information (date, wm_yr_wk).
- Integrated historical pricing data using store_id, item_id, and wm_yr_wk.

### Applied the pipeline to all remaining departments:-
- FOODS_2
- FOODS_3
- HOUSEHOLD_1
- HOUSEHOLD_2
- HOBBIES_1
- HOBBIES_2
Exported department-wise processed datasets to the processed folder.
Validated dataset shapes, columns, and successful file generation.

### Final Dataset Statistics
### Department	      Rows	   Columns
- FOODS_1_processed	4,132,080	   11
- FOODS_2_processed	7,613,740	   11
- FOODS_3_processed	15,743,990	 11
- HOUSEHOLD_1_processed	10,177,160	11
- HOUSEHOLD_2_processed	9,851,950	11
- HOBBIES_1_processed	7,958,080	 11
- HOBBIES_2_processed	2,850,370	 11

### Key Achievement

Successfully processed and validated more than 58 million retail transaction records, creating forecasting-ready datasets that will be used in the next phase for feature engineering, demand forecasting, and inventory optimization.

### Outcome:-
Successfully generated forecasting-ready datasets for all 7 retail departments containing sales, calendar, and pricing information.

---

# Day 5- Phase-5 :- Feature Engineering FOODS1 [Part 1]

### Feature Engineering – FOODS_1 Department

In this phase, forecasting-oriented features were created from the processed FOODS_1 dataset. The goal was to transform raw sales data into a machine-learning-ready dataset capable of capturing seasonality, demand trends, historical behavior, and price impact.

The date column was converted into datetime format and multiple calendar features such as year, month, day_of_week, and weekend_flag were generated. These features help identify weekly and seasonal demand patterns.

To incorporate historical demand information, lag features (7, 14, and 28 days) were created. Rolling mean features were then generated to capture short-term and long-term sales trends. Additionally, rolling standard deviation features were added to measure demand volatility and variability across different time windows.

A price_change_pct feature was also created to monitor product price fluctuations and study their impact on sales demand.

After feature generation, the dataset was validated through shape checks, null value analysis, and feature verification. The final dataset expanded from 11 columns to 25 columns and was saved as a feature-engineered dataset for future forecasting and inventory optimization tasks.

This notebook serves as a validated feature engineering workflow that can later be applied to the remaining departments using the same reusable pipeline.

## Feature Engineering Summary (FOODS_1)

## Objective
The objective of this notebook was to create forecasting-ready features from the processed FOODS_1 dataset. These features help machine learning and time-series forecasting models capture seasonality, demand patterns, trends, and price behavior.

## Dataset Information

- Department: FOODS_1
- Total Records: 4,132,080
- Original Columns: 11
- Final Columns: 25

## Features Created

### 1. Calendar Features
- year
- month
- day_of_week
- weekend_flag

Purpose:
Capture seasonal patterns, monthly demand variations, and weekend purchasing behavior.

### 2. Lag Features
- sales_lag_7
- sales_lag_14
- sales_lag_28

Purpose:
Provide historical sales information from previous periods to improve forecasting accuracy.

### 3. Rolling Mean Features
- rolling_mean_7
- rolling_mean_14
- rolling_mean_28

Purpose:
Capture short-term and long-term sales trends using moving averages.

### 4. Price Feature
- price_change_pct

Purpose:
Measure percentage change in product price over time and analyze its impact on demand.

### 5. Rolling Standard Deviation Features
- rolling_std_7
- rolling_std_14
- rolling_std_28

Purpose:
Measure demand volatility and sales variability across different time windows.

## Data Validation

- Shape Verified
- Feature Creation Verified
- Null Values Checked
- Lag Features Validated
- Rolling Features Validated
- Price Features Validated

## Output

Feature-engineered dataset successfully created and saved for forecasting and inventory optimization modeling.

---

# Day 6- Phase-6 :- Time Series EDA & Forecasting Phase
## Forecasting EDA & Prophet Dataset Preparation
### Tasks Completed
- Aggregated daily sales data from FOODS_1 department.
- Performed monthly and yearly trend analysis.
- Identified seasonality patterns in sales.
- Conducted weekday/weekend demand analysis.
- Visualized sales distribution using histogram and KDE plots.
- Detected outliers using boxplots.
- Validated forecasting suitability through trend and seasonality checks.
- Prepared Prophet-compatible dataset (ds, y format).
- Verified no missing values in forecasting dataset.
- Saved final forecasting-ready dataset.

### Key Insights
- Sales show a clear upward trend.
- December is the highest-performing month.
- Weekend demand is significantly higher than weekday demand.
- Saturday has the highest average sales.
- Dataset contains sufficient historical observations (1,913 days) for forecasting.

### Time Series EDA & Prophet Dataset Preparation Summary

## Objective
The objective of this notebook was to analyze the sales behavior of the FOODS_1 department before building a forecasting model and to prepare a clean dataset for Prophet forecasting.

## Work Completed

### 1. Daily Sales Aggregation
- Aggregated item-level sales into daily sales.
- Created a time series dataset with 1,913 daily observations.
- Verified there were no missing dates or missing sales values.

### 2. Trend Analysis
- Analyzed monthly and yearly sales trends.
- Observed a clear upward sales trend from 2011 to 2015.
- Identified business growth over time.

### 3. Seasonality Analysis
- Monthly sales patterns showed recurring fluctuations.
- Highest sales month: December 2015.
- Seasonal demand patterns were visible in the data.

### 4. Day-wise Sales Analysis
- Compared average sales across weekdays.
- Saturday recorded the highest average demand.
- Monday recorded the lowest average demand.
- Confirmed a strong weekend effect.

### 5. Distribution Analysis
- Examined sales distribution using histogram and density plots.
- Most daily sales values were concentrated between 2,000 and 3,500 units.
- Sales distribution was slightly right-skewed.

### 6. Outlier Analysis
- Used boxplots to identify unusual sales spikes.
- Found a few high-demand periods, which are normal for retail sales.

### 7. Prophet Dataset Preparation
- Converted dataset into Prophet format:
    - ds = Date
    - y = Sales
- Created a clean forecasting dataset with no missing values.
- Saved the final dataset for model training.

## Key Findings
- Upward sales trend exists.
- Seasonality exists.
- Weekend effect exists.
- Forecasting is suitable for this dataset.
- Prophet can be used as the forecasting model.

## Output File
foods_1_prophet_ready.csv

---

# Day 7- Phase-7 :- Prophet Forecasting Phase

### Completed Tasks

- Loaded FOODS_1 feature engineered dataset
- Aggregated sales at daily level
- Converted data into Prophet format (ds, y)
- Performed time-based train-test split
- Trained Facebook Prophet forecasting model
- Generated future demand predictions
- Evaluated model performance

### Model Performance

- MAE: 368.30
- RMSE: 472.83
- MAPE: 12.95%

### Insights

- Strong weekly seasonality detected
- Weekend sales higher than weekdays
- Stable long-term upward demand trend
- Prophet captured trend and seasonality effectively

### Status
- Prophet Baseline Model Completed

### Conclusion
The Prophet model achieved good forecasting performance and is suitable as the baseline forecasting model for retail demand prediction.

---

# Day 8- Phase-8 :- LightGBM Forecasting Model Phase
## LightGBM Forecasting – FOODS_1

### Work Completed
- Loaded FOODS_1 Prophet-ready dataset.
- Prepared forecasting feature set.
- Applied time-series train-test split.
- Trained LightGBM Regressor model.
- Generated 30-day sales predictions.
- Evaluated forecasting performance.
- Created Actual vs Predicted comparison table.
- Saved prediction results for future analysis.

### Features Used
- Time Features
- Lag Features
- Rolling Mean Features
- Rolling Standard Deviation Features
- Weekend Indicator

### Results
- MAE: 234.92
- RMSE: 328.54
- MAPE: 7.41%
- Forecast Accuracy: 92.59%

### Key Insight
LightGBM achieved significantly better forecasting performance than Prophet and is currently the best-performing model for FOODS_1 demand forecasting.

### Output
- foods_1_lightgbm_predictions.csv

---

