# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output:
```
import pandas as pd
import numpy as np
from scipy.stats import zscore
```
```
df = pd.read_csv("/content/Loan_data.csv")
```
```

print("Original Dataset:")
print(df)
```
<img width="942" height="828" alt="image" src="https://github.com/user-attachments/assets/a1389528-94a5-4735-ba72-fae6763d095b" />

```
print("\nDataset Information:")
print(df.info())
```
<img width="722" height="535" alt="image" src="https://github.com/user-attachments/assets/9c4f4709-85fc-4f82-8ec8-dd6c830e778b" />

```
print("Missing Values:")
print(df.isnull().sum())
```

<img width="357" height="402" alt="image" src="https://github.com/user-attachments/assets/30d263d4-d75c-4b26-a26c-0531606c6b1a" />

```
df_clean = df.dropna()
print("\nDataset After Removing Null Values:")
print(df_clean)
```
<img width="1098" height="835" alt="image" src="https://github.com/user-attachments/assets/5179f94a-271e-4ea2-870f-1c43baa3ca10" />

```

df_clean.to_csv("cleaned_data.csv", index=False)
numeric_cols = df_clean.select_dtypes(include=np.number).columns
df_iqr = df_clean.copy()

```

```
for col in numeric_cols:
    Q1 = df_iqr[col].quantile(0.25)
    Q3 = df_iqr[col].quantile(0.75)
    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    df_iqr = df_iqr[
        (df_iqr[col] >= lower) &
        (df_iqr[col] <= upper)
    ]
```

```

print("\nIQR Outlier Removal:")
print(df_iqr)

```

<img width="986" height="825" alt="image" src="https://github.com/user-attachments/assets/c00d573a-1787-4b99-be24-a8df6bdfb1d8" />

```

df_iqr.to_csv("iqr_cleaned_data.csv", index=False)
df_zscore = df_clean.copy()
for col in numeric_cols:
    if df_zscore.empty:
        break

    scores = zscore(df_zscore[col], nan_policy="omit")
    df_zscore = df_zscore[np.abs(scores) < 3]

```
```

print("\nZ-score Outlier Removal:")
print(df_zscore)

```
<img width="970" height="810" alt="image" src="https://github.com/user-attachments/assets/21bc9a68-5ddd-4c80-ae05-6bd76f3d05bc" />

## DATA 

```

df = pd.read_csv("/content/Data_set.csv")

```
```

print("Original Dataset:")
print(df)
```
<img width="1022" height="810" alt="image" src="https://github.com/user-attachments/assets/f27f586c-543a-4034-844e-c24beb67637a" />

```

print("\nDataset Information:")
print(df.info())

```
<img width="856" height="408" alt="image" src="https://github.com/user-attachments/assets/c93af9f6-0024-42f1-a4d2-cf2238ec01a3" />

```

print("\nMissing Values:")
print(df.isnull().sum())

```
<img width="637" height="302" alt="image" src="https://github.com/user-attachments/assets/08a7050e-d792-4114-b507-c0919be3f844" />

```
df_clean = df.dropna()

print("\nDataset After Removing Null Values:")
print(df_clean)

```
<img width="792" height="852" alt="image" src="https://github.com/user-attachments/assets/901b182a-7cc4-47ba-961c-cd91c349355a" />

```

df_clean.to_csv("cleaned_data.csv", index=False)
numeric_cols = df_clean.select_dtypes(include=np.number).columns
df_iqr = df_clean.copy()
for col in numeric_cols:
    Q1 = df_iqr[col].quantile(0.25)
    Q3 = df_iqr[col].quantile(0.75)
    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    df_iqr = df_iqr[
        (df_iqr[col] >= lower) &
        (df_iqr[col] <= upper)
    ]

```
```

print("\nIQR Outlier Removal:")
print(df_iqr)

```
<img width="951" height="802" alt="image" src="https://github.com/user-attachments/assets/c275b184-34e7-45a6-be76-689b5c28b559" />

```

df_iqr.to_csv("iqr_cleaned_data.csv", index=False)
df_zscore = df_clean.copy()
for col in numeric_cols:
    if df_zscore.empty:
        break

    scores = zscore(df_zscore[col], nan_policy="omit")
    df_zscore = df_zscore[np.abs(scores) < 3]

```

```

print("\nZ-score Outlier Removal:")
print(df_zscore)

```
<img width="905" height="812" alt="image" src="https://github.com/user-attachments/assets/1eedb9aa-78b2-4a29-843a-241e259d8d13" />


```
df_zscore.to_csv("zscore_cleaned_data.csv", index=False)

print("\nAll operations completed successfully.")
```
<img width="965" height="222" alt="image" src="https://github.com/user-attachments/assets/e8b0595f-5b72-4b8e-8fb8-b5d57c54dc14" />


### SUMMARY:

The process begins by importing the libraries pandas (for handling tables), numpy (for numerical operations) and zscore from scipy (for outlier detection). The loan dataset is then loaded from a CSV file into a DataFrame, which holds 367 loan applicants and 12 columns such as Gender, ApplicantIncome, LoanAmount and Credit_History. The data is inspected with df.info(), which shows each column’s data type and non-null count. For example, Credit_History has only 338 non-null values out of 367, so some entries are missing.

Next, missing values (NaN) are counted with df.isnull().sum(). Credit_History has 29 missing, Self_Employed has 23, Gender has 11, Dependents has 10, Loan_Amount_Term has 6 and LoanAmount has 5. These are removed with df.dropna(), which deletes every row containing at least one missing value. For example, an applicant whose Credit_History is blank is dropped entirely, even if all their other details are filled in. This reduces the data from 367 to 289 rows and is saved as cleaned_data.csv.

After that, the numeric columns (ApplicantIncome, CoapplicantIncome, LoanAmount, Loan_Amount_Term and Credit_History) are selected, because outliers only apply to numbers. Outliers are unusually extreme values. For example, an applicant with an income of 80,000 when most earn around 4,000 would distort the analysis.

The IQR method calculates Q1 (25th percentile), Q3 (75th percentile) and IQR = Q3 − Q1. Any value below Q1 − 1.5×IQR or above Q3 + 1.5×IQR is treated as an outlier, and its row is removed. For example, a very high LoanAmount or an unusual Loan_Amount_Term (such as 180 when most are 360) gets removed. This leaves 188 rows, saved as iqr_cleaned_data.csv.

The Z-score method measures how many standard deviations a value is from the column’s mean. Rows with a Z-score of 3 or more (in absolute value) are removed. This is more lenient and leaves 271 rows, saved as zscore_cleaned_data.csv.


            
# Result
Thus, the data cleaning process was successfully performed on the Loan_data.csv dataset using Python. Missing values were removed, and outliers were detected and removed using the IQR and Z-score methods. The cleaned datasets were saved as CSV files for further analysis.
       
