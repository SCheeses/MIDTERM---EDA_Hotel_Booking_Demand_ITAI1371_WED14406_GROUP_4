Hotel Booking Data Cleanup and Preparation Project

## Project Overview
This project focuses on cleaning and preparing the **Hotel Booking Demand** dataset for future machine learning use. The selected machine learning problem is **predicting whether a hotel booking will be canceled** using the target variable `is_canceled`.

The project follows the course requirements for:
- handling missing values
- scaling numeric data
- normalizing selected skewed features
- encoding categorical variables
- applying feature engineering
- splitting the data into training and testing sets
- demonstrating the dataset before and after preprocessing in a Jupyter notebook

This repository contains the final deliverables for the midterm submission.

## Repository Structure
```text
hotel-booking-midterm/
├── README.md
├── dataset_source.md
├── proposal.pdf
├── reflection_journal.md
├── hotel_booking_EDA.ipynb
└── link_to_cleaned_dataset.md
```


## Original Dataset
- **Dataset name:** Hotel Booking Demand Dataset 
- **Original source:** Kaggle
- **Target variable:** `is_canceled`

The purpose of this dataset preparation is to support a future classification model that predicts whether a booking will be canceled.

## Machine Learning Goal
The machine learning goal for this project is to build a **classification** model in the future that predicts whether a booking will be canceled.

Based on exploratory data analysis, the strongest **promising predictors identified through EDA** include:
- `lead_time`
- `deposit_type`
- `adr` (average daily rate)
- `market_segment`
- `customer_type`
- `previous_cancellations`
- `total_nights`

These variables appeared likely to influence cancellation behavior and were retained or engineered as part of the preprocessing workflow.

## Preprocessing Steps Completed
The following data-cleaning and preparation steps were completed:

### 1. Train/Test Split
The original raw dataset was split into:
- **70% training data**
- **30% testing data**

EDA was performed only on the training set to avoid data leakage.

### 2. Missing Value Handling
Missing values were filled using logical strategies:
- `children` filled with `0`
- `country` filled with the most frequent value from training data
- `agent` filled with `0`
- `company` filled with `0`

### 3. Feature Engineering
New features were created to improve the usability of the dataset:
- `total_guests`
- `total_nights`
- `has_agent`
- `has_company`
- `arrival_month_num`
- `is_family`

### 4. Leakage Prevention
The following columns were removed because they were too directly tied to the final booking outcome:
- `reservation_status`
- `reservation_status_date`

### 5. Encoding
Categorical columns were converted into numeric format using **one-hot encoding**.

### 6. Normalization and Scaling
Selected skewed numeric features were transformed where appropriate, and numeric columns were scaled for future machine learning use.

**Note:** `adr` was **scaled only** and was **not log-transformed** in the final corrected workflow.
