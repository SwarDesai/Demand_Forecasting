**Store Demand Forecasting**

**Overview**

This project focuses on forecasting the demand for items in various stores over time. Using 5 years of historical sales data for 50 different items across 10 stores, we build a predictive model using LightGBM. The goal is to accurately predict future sales, which is crucial for inventory management, supply chain optimization, and overall business planning.

The notebook walks through the process of data exploration, feature engineering, model training, and evaluation.

**Dataset**

The dataset consists of a train.csv file with the following columns:

- **date**: The date of the sales record.

- **store**: A unique identifier for the store (1-10).

- **item**: A unique identifier for the item (1-50).

- **sales**: The number of items sold on that date at that store.

The data spans from January 1, 2013, to December 31, 2017.

**Exploratory Data Analysis (EDA)**

The initial analysis of the data revealed several key insights:

- Dataset Size: The training data contains 913,000 records.

- Monthly Sales Trend: Sales show a clear seasonal pattern, typically peaking in the middle of the year (July) and hitting a low point at the beginning and end of the year.

- Sales by Store: While all stores follow a similar seasonal trend, their sales volumes differ, indicating store-specific patterns.

**Feature Engineering**

To enhance the model's predictive power, several new features were created from the existing data:

- Time-Based Features:

  - month: To capture monthly seasonality.

  - day_of_week: To capture weekly sales patterns.

- Lag Features: Sales data from previous time periods (e.g., 91, 182, 364 days ago) were used to capture long-term seasonality and trends.

- Rolling Mean Features: The rolling mean of sales over different window sizes (e.g., 365, 546 days) was calculated to smooth out short-term fluctuations and identify the underlying trend.

- Exponentially Weighted Mean (EWM) Features: EWM was used to give more weight to recent sales data, making the model more responsive to recent trends.

- Random Noise: A small amount of random noise was added to the lag features to help prevent overfitting.

**Modeling**
- Algorithm: A LightGBM (Light Gradient Boosting Machine) model was used for its efficiency and high performance with tabular data.

- Training and Validation:

  - The data was split into a training set (before July 1, 2017) and a validation set (July 1, 2017, to Dec 31, 2017).

  - The sales target variable was transformed using np.log1p to stabilize variance and handle skewed data, a common practice for demand forecasting.

- Evaluation Metric: The model's performance was evaluated using the Symmetric Mean Absolute Percentage Error (SMAPE), which is a good metric for forecast accuracy. The custom SMAPE function is defined in the notebook.

**Results**

The trained LightGBM model achieved a SMAPE of approximately 11.91% on the validation set.

The plot below shows a comparison of the actual sales versus the predicted sales for a sample item, demonstrating the model's ability to capture the sales patterns accurately.

