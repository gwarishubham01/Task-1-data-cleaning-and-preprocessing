# Task-1-data-cleaning-and-preprocessing

**Objective**: Clean and prepare a raw dataset(with nulls, duplicates, inconsistent formats).
**Dataset from Kaggle for Task 1:**  
Dataset: <a href="https://github.com/gwarishubham01/Task-1-data-cleaning-and-preprocessing/blob/main/marketing_campaign.csv">Dataset</a>   

## **Importing Libraries and Load Data**

- Loading essential libraries (Pandas, NumPy, datetime)
```Python
import numpy as np
import pandas as pd
from datetime import datetime

import warnings
warnings.filterwarnings('ignore')
```
- Reading dataset from CSV with tab separator
```python
df = pd.read_csv("/content/sample_data/marketing_campaign.csv", sep='\t')
df.head()
```
![Screenshot (64)](https://github.com/user-attachments/assets/dfc3485f-c796-44c2-b8b7-ef68dee6f861)
## **Data Exploration**
- Dataset contains 2240 rows and 29 column (or features)
- Income has 24 missing values
```Python
df.describe().T
```
![Screenshot (65)](https://github.com/user-attachments/assets/4e5d65aa-6786-4074-8114-ec3cc19ffa57)

```Python
df.info()
```
![Screenshot (66)](https://github.com/user-attachments/assets/996eba4f-6986-4e6d-a17d-7a77f5a363eb)

## **Data Cleaning and Preprocessing**

### ✅ **1. Identify and Handle Missing Values**
- Used `.isnull()` to detect missing values in the "Income" column.
```python
df[df["Income"].isnull()].index
```
![Screenshot (67)](https://github.com/user-attachments/assets/3ceaefd2-2c2d-453c-8f06-d06470f0d75e)

- Replaced missing values with the **mean** of the column.
```python
df["Income"] = df["Income"].fillna(df["Income"].mean())
```
- Checking for any missing values
```python
df[df["Income"].isnull()].index
```
![Screenshot (68)](https://github.com/user-attachments/assets/d4cd4682-d399-4807-aa89-6af6ed7ea567)

### ✅ **2. Remove Duplicate Rows**
```python
df = df.drop_duplicates()
df.info()
```
- All duplicate rows in the dataset are removed using `.drop_duplicates()`
![Screenshot (69)](https://github.com/user-attachments/assets/f37aad22-cf41-4008-8516-c30094a3657b)



### ✅ **3. Standardize Text Values**
```python
numerical_columns=df.select_dtypes(include = 'number').columns
categorical_columns=df.select_dtypes(include = 'object').columns
```
```python
df[categorical_columns] =df[categorical_columns].astype('category')
categorical_columns
```
![Screenshot (70)](https://github.com/user-attachments/assets/1bd06681-54ba-4542-b914-35df8e046400)

```python
df['Education'].unique()
```
![Screenshot (71)](https://github.com/user-attachments/assets/19782bec-57ab-45ee-93e7-3db95440e825)
```python
df['Marital_Status'].unique()
```
![Screenshot (72)](https://github.com/user-attachments/assets/b0e70b8c-d138-4ac6-b85a-82710bf66118)

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
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')
```
### ✅ **6. Check and Fix Data Types**
```python
df.info()
```
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
![Screenshot (73)](https://github.com/user-attachments/assets/9c9fa424-9e46-44ac-a144-bc1ce2d1b7b0)
