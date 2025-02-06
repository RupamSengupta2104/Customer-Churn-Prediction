Customer Churn Prediction for Telecom Company
Project Overview
This project aims to predict customer churn for a telecom company. The focus is on cleaning and preparing the dataset before performing any analysis or machine learning. In this phase, we will be performing data cleaning tasks like handling missing values, identifying duplicates, and preparing the dataset for the modeling process.

1. Setup Environment
To get started, you'll need to install the required Python libraries. You can do this using pip:

bash
Copy
Edit
pip install pandas numpy
Pandas: For data manipulation and analysis.
Numpy: For numerical operations and handling missing data.
2. Load the Dataset
First, we load the dataset into a DataFrame:

python
Copy
Edit
import pandas as pd

# Load the dataset
df = pd.read_csv("telecom_customer_churn.csv")
Here, telecom_customer_churn.csv is the CSV file containing the telecom customer data. This file should be placed in your working directory.

3. Check for Duplicates
Before we move on to the data cleaning process, it's important to check if there are any duplicate rows in the dataset.

python
Copy
Edit
# Check for duplicate rows
print(df.duplicated().sum())
Explanation:

df.duplicated() returns a boolean Series indicating whether each row is a duplicate.
sum() counts how many rows are duplicates.
If any duplicates are found, you can remove them using:

python
Copy
Edit
df.drop_duplicates(inplace=True)
4. Handle Missing Values
Why is this important?
Missing data can break machine learning models.
We need to handle missing values by either filling or removing them.
Check for Missing Values
python
Copy
Edit
# Check for missing values
print(df.isnull().sum())
This will print the number of missing values for each column in the dataset.

Fix Missing Values
Based on the data types of each column, we'll handle missing values differently.

Numerical Columns:
For numerical columns like Avg Monthly Long Distance Charges and Avg Monthly GB Download, we replace missing values with the mean of that column.

python
Copy
Edit
# Fix missing values in numerical columns using mean
df['Avg Monthly Long Distance Charges'] = df['Avg Monthly Long Distance Charges'].fillna(df['Avg Monthly Long Distance Charges'].mean())
df['Avg Monthly GB Download'] = df['Avg Monthly GB Download'].fillna(df['Avg Monthly GB Download'].mean())
Categorical Columns:
For categorical columns like Offer, Multiple Lines, and Churn Category, we replace missing values with the mode (most frequent value) of that column.

python
Copy
Edit
# Fix missing values in categorical columns using mode
categorical_columns = ['Offer', 'Multiple Lines', 'Internet Type', 'Online Security',
                       'Online Backup', 'Device Protection Plan', 'Premium Tech Support',
                       'Streaming TV', 'Streaming Movies', 'Streaming Music',
                       'Unlimited Data', 'Churn Category', 'Churn Reason']

for col in categorical_columns:
    df[col] = df[col].fillna(df[col].mode()[0])
Explanation:

Numerical columns: We use the mean because it represents the average value, which is good for numerical data.
Categorical columns: We use the mode because it represents the most frequent category in the data, which is ideal for categorical values.
5. Verify Missing Values Are Handled
To make sure that all missing values have been handled properly, you can recheck the missing values count:

python
Copy
Edit
# Verify missing values are fixed
print(df.isnull().sum())
If this shows all zeros, then you've successfully handled all the missing data.

6. Save the Cleaned Dataset
It's always a good idea to save your cleaned dataset for future use.

python
Copy
Edit
df.to_csv("cleaned_customer_churn.csv", index=False)
Explanation:

This saves the cleaned data to a new CSV file called cleaned_customer_churn.csv.
index=False ensures that the row indices are not saved in the CSV file
