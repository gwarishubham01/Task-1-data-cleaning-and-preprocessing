# Task-1-data-cleaning-and-preprocessing

**Objective**: Clean and prepare a raw dataset(with nulls, duplicates, inconsistent formats).
**Dataset from Kaggle for Task 1:**  
Dataset: <a href="https://github.com/gwarishubham01/Task-1-data-cleaning-and-preprocessing/blob/main/marketing_campaign.csv">Dataset</a>   

## **Importing Libraries and Load Data**
- Loading essential libraries (Pandas, NumPy, datetime)
- Reading dataset from CSV with tab separator
```Python
import numpy as np
import pandas as pd
from datetime import datetime

import warnings
warnings.filterwarnings('ignore')

df = pd.read_csv("/content/sample_data/marketing_campaign.csv", sep='\t')
```
## **Data Exploration**
- Dataset contains 2240 rows and 29 column (or features)
- Income has 24 missing values
```Python
df.head()
df.describe().T
df.info()
```

## **Data Cleaning and Preprocessing**

### ✅ **1. Identify and Handle Missing Values**
**Python Implementation:**

```python
df[df["Income"].isnull()].index
df["Income"] = df["Income"].fillna(df["Income"].mean())
```
- Used `.isnull()` to detect missing values in the "Income" column.
- Replaced missing values with the **mean** of the column.


### ✅ **2. Remove Duplicate Rows**
```python
df = df.drop_duplicates()
```
- All duplicate rows in the dataset are removed using `.drop_duplicates()`



### ✅ **3. Standardize Text Values**
```python
df['Marital_Status'] = df['Marital_Status'].replace(['Together', 'Married'], 'Couple')
df['Marital_Status'] = df['Marital_Status'].replace(['Divorced', 'Widow', 'Alone', 'Absurd', 'YOLO'], 'Single')
```
- **Marital_Status** categories were consolidated into `'Couple'` and `'Single'`.




### ✅ **4. Convert Date Formats**
```python
df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'] ,format='%d-%m-%Y')
```




### ✅ **5. Rename Column Headers to Be Clean and Uniform**

```python
df.columns = df.columns.str.lower().str.replace(' ', '_')
```



### ✅ **6. Check and Fix Data Types**
```python
df.info()
```
- You’ve checked data types with `.info()`.
```python
df[categorical_columns] = df[categorical_columns].astype('category')
```
- Converted `object` types to `category`.

To ensure `Year_Birth` is integer and dates are datetime:
```python
df['Year_Birth'] = df['Year_Birth'].astype(int)
```

- Export cleaned data:
  ```python
  df.to_csv("cleaned_marketing_campaign.csv", index=False)
  ```
