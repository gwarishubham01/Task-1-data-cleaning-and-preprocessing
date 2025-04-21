# Task-1-data-cleaning-and-preprocessing

### **Objective**: Clean and prepare a raw dataset(with nulls, duplicates, inconsistent formats).
Dataset from Kaggle for Task 1:
Dataset:
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
- All duplicate rows in the dataset are removed using `.drop_duplicates()`.



### ✅ **3. Standardize Text Values**
```python
df['Marital_Status'] = df['Marital_Status'].replace(['Together', 'Married'], 'Couple')
df['Marital_Status'] = df['Marital_Status'].replace(['Divorced', 'Widow', 'Alone', 'Absurd', 'YOLO'], 'Single')
```
- **Marital_Status** categories were consolidated into `'Couple'` and `'Single'`.

> You could also standardize columns like `'Education'`, `'Country'`, or others if needed.



### ✅ **4. Convert Date Formats**
```python
df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'] ,format='%d-%m-%Y')
```
- The **Dt_Customer** column was converted into `datetime` format.



### ⚠️ **5. Rename Column Headers to Be Clean and Uniform**
This was **not yet handled** in the code. You can add:
```python
df.columns = df.columns.str.lower().str.replace(' ', '_')
```
- This will convert all column names to lowercase and replace spaces with underscores.



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



### 💡 Suggestions to Enhance Further:
- **Standardize gender or country names** if present.
- **Normalize column values** (e.g., lowercase text entries).
- Consider checking **outliers** in income or age.
- Export cleaned data:
  ```python
  df.to_csv("cleaned_marketing_campaign.csv", index=False)
  ```
