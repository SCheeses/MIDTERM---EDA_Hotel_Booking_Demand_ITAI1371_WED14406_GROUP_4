# Hotel Booking Cleanup Project Reflection Journal

## Team Members
- Jade
- Kate
- Alexia
- Cherluk

## Project Overview
For this midterm project, our team selected the **Hotel Booking Demand** dataset and prepared it for a future machine learning task. The main goal of the project was to clean the raw data, split it into training and testing sets, perform exploratory data analysis (EDA) on the training data only, and apply preprocessing steps so the dataset would be ready for later model building. We selected **booking cancellation (`is_canceled`)** as the future machine learning target because it is a clear classification problem and because many of the features in the dataset could logically help explain cancellation behavior.

## Dataset Source
- Original dataset: Hotel Booking Demand dataset from Kaggle
- Dataset used for this project: `hotel_bookings.csv`

## What We Accomplished
Our team completed the following main tasks:

1. **Preserved the original dataset** without manually editing it.
2. **Split the raw dataset into training and testing sets** using a 70%/30% split.
3. **Performed EDA on the training set only** to avoid data leakage.
4. **Handled missing values** in columns such as `children`, `country`, `agent`, and `company` using logical fill methods.
5. **Engineered useful features** such as total guests, total nights, family indicator, and indicators for whether an agent or company was involved.
6. **Removed leakage columns** that could unfairly reveal the answer, including `reservation_status` and `reservation_status_date`.
7. **Encoded categorical variables** using one-hot encoding.
8. **Transformed and scaled numeric variables** where appropriate so the cleaned data would be usable for a future ML model.
9. **Exported cleaned datasets** for training, testing, and full-dataset use.

## Individual Contributions
### Jade
Jade completed the first major draft of the project work and created the initial notebook and write-up foundation. She helped define the project direction, selected the hotel booking dataset as a workable option for the assignment, and contributed to the early cleanup workflow. Jade also made early judgment calls about preserving rows by filling missing values instead of deleting large parts of the dataset.

### Kate
Kate completed the correction and integration pass on the project deliverables. This included reviewing the notebook logic against the exported cleaned CSV files, correcting preprocessing inconsistencies, refining the workflow so the split happened before EDA, and making sure the written deliverables matched the actual final pipeline. Kate also revised the reflection journal and coordinated the final submission materials.

### Alexia
Alexia contributed to reviewing the preprocessing workflow, especially the handling of categorical variables and feature engineering decisions. She helped support the logic for using one-hot encoding instead of assigning arbitrary numeric labels, and she contributed to reviewing whether the engineered features were useful and easy to justify.

### Cherluk
Cherluck contributed to checking the consistency of the numeric preprocessing steps and supported the review of the final outputs. This included reviewing transformation choices for skewed numeric variables and helping verify that the notebook explanations, cleaned datasets, and final written materials matched each other.

## Challenges, Judgment Calls, and Reasoning
A major part of this project involved making judgment calls rather than just following a single fixed recipe. Below are some of the main decisions we worked through and the logic behind them.

### Jade — choosing the ML goal from the dataset
One of the first judgment calls was deciding what problem the dataset should solve. The hotel bookings dataset could support different questions, such as predicting cancellation, predicting average daily rate, or studying seasonal booking behavior. Jade helped frame the project around predicting `is_canceled` because it is a clear target column, it fits a classification problem well, and many of the other features in the dataset could logically help explain cancellation behavior. This made the project more focused and more appropriate for a future machine learning exercise.

### Jade — deciding what to do with missing values instead of deleting rows
Another early judgment call was deciding whether missing values should be filled in or whether rows should be removed. Jade’s initial work leaned toward preserving as much data as possible because dropping too many rows could shrink the dataset and remove potentially useful patterns. The team agreed this was the better choice because the assignment emphasized cleanup and preparation, not simply deleting messy data. For that reason, we used logical replacements such as `0` for columns like `children`, `agent`, and `company`, and a most-frequent-value approach for `country`.

### Kate — deciding to split before doing EDA and preprocessing
One important judgment call was the order of operations. It would have been easier to explore and clean the entire dataset at once, but that risks data leakage. Kate pushed the corrected workflow so the raw dataset was split into 70% training and 30% testing first, and then EDA was performed only on the training data. The reasoning was that the testing set should stay untouched until the end so that it can act like “new” data for a future machine learning model. This decision made the project more methodologically correct.

### Kate — deciding which columns created leakage and should be removed
Another challenge was deciding whether every column in the raw dataset was fair to keep. Kate identified that columns such as `reservation_status` and `reservation_status_date` were too closely tied to the final outcome and would basically give away the answer to whether a booking was canceled. The judgment call was to remove them, even though they may look informative at first glance. The logic was that machine learning features should help predict the target fairly, not reveal it directly.

### Alexia — deciding how to handle categorical variables
A challenge in the project was figuring out what to do with text-based columns like hotel type, meal plan, market segment, and room type. Alexia worked through the choice between label encoding and one-hot encoding. The group went with one-hot encoding because most of these categories do not have a true numeric order, and assigning them numbers like 1, 2, and 3 could accidentally imply ranking. One-hot encoding was the more logical option because it lets the model treat categories as separate groups rather than pretending one category is “higher” than another.

### Alexia — deciding what counted as useful feature engineering
Feature engineering required judgment because not every new column improves a dataset. Alexia helped identify combinations of raw features that would be more meaningful than the originals alone, such as `total_guests`, `total_nights`, `has_agent`, `has_company`, and `is_family`. The reasoning was that these engineered columns summarize real booking behavior more clearly than scattered raw columns do by themselves. This improved the usability of the dataset while still keeping the transformations easy to explain.

### Cherluk — deciding which numeric columns needed transformation
One technical challenge was determining whether all numeric columns should be treated the same way. Cherluck helped review which variables were skewed and therefore candidates for normalization or transformation. The team’s reasoning was that some variables, such as `lead_time` and `days_in_waiting_list`, had very uneven distributions, so they were stronger candidates for transformation than more balanced columns. This judgment call mattered because preprocessing should respond to the shape of the data rather than applying the same method blindly to every numeric feature.

### Cherluk — catching consistency issues between notebook logic and output files
Another challenge was making sure the notebook, the explanation, and the exported cleaned CSV files all matched each other. Cherluck helped review the final consistency of the project and supported the correction process when it became clear that one variable, `adr`, had been described as log-transformed in the notebook even though the final files reflected scaling only. The logic behind fixing that mismatch was that reproducibility matters: the written explanation, code, and deliverables should all tell the same story.

### Shared team challenge — balancing best practice with simplicity
A recurring challenge across the project was choosing methods that were technically sound but still understandable and defendable for a midterm assignment. In several places, we chose simpler, transparent methods over more complicated ones because the goal was not just to produce a cleaned dataset, but to show that we understood why each preprocessing step was used.

## What We Learned from EDA
Our EDA did not build a final machine learning model, but it did help us identify patterns that may be useful later. Based on the training data, we observed that several features appeared likely to be strong predictors of booking cancellation. These included:

- `lead_time`
- `deposit_type`
- `adr` (average daily rate)
- `market_segment`
- `customer_type`
- `previous_cancellations`
- `total_nights`

These features were considered promising because they showed logical relationships to booking behavior. For example, reservations made far in advance may be more likely to change, customers with a history of previous cancellations may be more likely to cancel again, and room pricing or deposit requirements may influence whether guests keep or cancel their reservations.

## Conclusion
Based on our exploratory data analysis, the strongest likely predictors of booking cancellation were variables related to booking behavior, customer history, and reservation details. Features such as **lead time**, **deposit type**, **ADR (average daily rate)**, **market segment**, **customer type**, **previous cancellations**, and **total nights** appeared especially important because they showed logical relationships to whether a booking might be canceled. For example, reservations made far in advance may be more likely to change, customers with a history of prior cancellations may be more likely to cancel again, and pricing or deposit requirements may influence whether guests keep or cancel their bookings. While this project did not build a final machine learning model, the EDA suggested that these variables would likely be among the most useful features for predicting the target variable, `is_canceled`.

Overall, this project helped us practice the full data preparation pipeline needed before machine learning: preserving the original data, splitting correctly, performing EDA on training data only, making decisions about missing values, engineering features, encoding categories, scaling numeric variables, and validating that the final outputs matched the documented workflow. The cleaned dataset is now in a form that can be used for a later classification model.
