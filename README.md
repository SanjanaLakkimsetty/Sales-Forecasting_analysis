# Sales Forecasting Project

## Overview

This project involves data analysis and visualization to understand and predict sales trends for a retail company. Various datasets including store transactions, oil prices, holidays, and events are used to gain insights and make forecasts.

## Datasets

1. **train.csv**: Contains historical sales data.
2. **test.csv**: Contains data to predict sales.
3. **oil.csv**: Contains daily oil prices.
4. **stores.csv**: Contains information about different stores.
5. **transactions.csv**: Contains transaction data for different stores.
6. **holidays_events.csv**: Contains information about holidays and events.
7. **sample_submission.csv**: A sample submission file in the format required for the competition.

## Libraries Used

- numpy
- pandas
- seaborn
- matplotlib
- polars
- scikit-learn

## Installation

To install the required libraries, run:

```bash
pip install numpy pandas seaborn matplotlib polars scikit-learn

## Data Loading
The data is loaded using pandas:

import pandas as pd

train = pd.read_csv("Data/train.csv")
test = pd.read_csv("Data/test.csv")
oil = pd.read_csv("Data/oil.csv")
stores = pd.read_csv("Data/stores.csv")
transactions = pd.read_csv("Data/transactions.csv")
holidays_events = pd.read_csv("Data/holidays_events.csv")
sample_submission = pd.read_csv("Data/sample_submission.csv")

## Data Preprocessing

Combine train and test datasets for easier preprocessing.
Convert date columns to datetime objects.
Extract year, month, day, day of the week, day name, quarter, and leap year information from date columns.
def datetime(df):
    df['date'] = pd.to_datetime(df["date"])
    df['year'] = df['date'].dt.year
    df['month'] = df['date'].dt.month
    df['day'] = df['date'].dt.day
    df['day_of_week'] = df['date'].dt.dayofweek
    df['day_name'] = df['date'].dt.day_name()
    df['quarter'] = df['date'].dt.quarter
    df['is_leap_year'] = df['date'].dt.is_leap_year
    return df

df = datetime(df)

##Data Analysis and Visualization
Visualizations were created to understand sales trends over time:
-Sales by Year, Month, Day, Day of Week, Day Name, and Quarter
import matplotlib.pyplot as plt

grouping_columns = ['year', 'month', 'day', 'day_name', 'quarter', 'day_of_week']
fig, axes = plt.subplots(3, 2, figsize=(12, 10))
axes = axes.flatten()

for ind, column in enumerate(grouping_columns):
    grouped_data = df.groupby(column)['sales'].sum()
    grouped_data.plot(ax=axes[ind], kind='bar', title=f'Sales by {column}')

plt.tight_layout()
plt.show()
