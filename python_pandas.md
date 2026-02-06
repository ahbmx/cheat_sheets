
```python
import pandas as pd
import numpy as np
```

---

## 1️⃣ Reading Files

### CSV

```python
df = pd.read_csv("data.csv")
```

```python
df = pd.read_csv("data.csv", sep=";", encoding="utf-8")
```

### Excel

```python
df = pd.read_excel("data.xlsx")
```

```python
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")
```

### JSON

```python
df = pd.read_json("data.json")
```

---

## 2️⃣ Quick Inspection

```python
df.head()        # first 5 rows
df.tail()        # last 5 rows
df.shape         # (rows, columns)
df.columns       # column names
df.dtypes        # data types
df.info()        # overview
df.describe()    # stats for numeric columns
```

---

## 3️⃣ Selecting Data

### Select Columns

```python
df["age"]
df[["name", "age"]]
```

### Select Rows

```python
df.loc[0]          # by index label
df.iloc[0]         # by position
df.iloc[0:5]       # slice
```

### Rows + Columns

```python
df.loc[df["age"] > 30, ["name", "salary"]]
```

---

## 4️⃣ Filtering (Very Common)

```python
df[df["age"] > 30]
```

```python
df[(df["age"] > 30) & (df["country"] == "US")]
```

```python
df[df["country"].isin(["US", "UK"])]
```

```python
df[df["name"].str.contains("John", na=False)]
```

---

## 5️⃣ Changing Values

### Change Single Value

```python
df.loc[0, "age"] = 35
```

### Replace Values

```python
df["gender"] = df["gender"].replace({"M": "Male", "F": "Female"})
```

### Change Values Based on Another Column

```python
df.loc[df["age"] >= 18, "is_adult"] = True
df.loc[df["age"] < 18, "is_adult"] = False
```

---

## 6️⃣ Creating New Columns

### From Existing Column

```python
df["salary_k"] = df["salary"] / 1000
```

### Based on Conditions (`np.where`)

```python
df["status"] = np.where(df["age"] >= 18, "adult", "minor")
```

### Multiple Conditions (`np.select`)

```python
conditions = [
    df["score"] >= 90,
    df["score"] >= 75,
    df["score"] < 75
]

choices = ["A", "B", "C"]

df["grade"] = np.select(conditions, choices)
```

### Using `apply`

```python
df["name_length"] = df["name"].apply(len)
```

```python
def classify_age(age):
    if age < 18:
        return "minor"
    elif age < 65:
        return "adult"
    else:
        return "senior"

df["age_group"] = df["age"].apply(classify_age)
```

---

## 7️⃣ Updating Values Based on Multiple Columns

```python
df.loc[
    (df["country"] == "US") & (df["salary"] > 100000),
    "tax_rate"
] = 0.30
```

```python
df["bonus"] = np.where(
    (df["department"] == "Sales") & (df["performance"] == "High"),
    5000,
    0
)
```

---

## 8️⃣ Handling Missing Values

```python
df.isna()
df.isna().sum()
```

```python
df.dropna()
df.fillna(0)
```

```python
df["age"] = df["age"].fillna(df["age"].mean())
```

---

## 9️⃣ Sorting & Grouping

### Sort

```python
df.sort_values("age", ascending=False)
```

### Group By

```python
df.groupby("country")["salary"].mean()
```

```python
df.groupby("department").agg({
    "salary": "mean",
    "age": "max"
})
```

---

## 🔟 Saving Files

```python
df.to_csv("output.csv", index=False)
```

```python
df.to_excel("output.xlsx", index=False)
```

---

## ⚡ Super Common Patterns (Memorize These)

```python
df.loc[condition, "column"] = value
```

```python
df["new_col"] = np.where(condition, true_value, false_value)
```

```python
df = df[df["column"] > x]
```

---

---
---

# 🧹 Pandas Data Cleaning Cheat Sheet

```python
import pandas as pd
import numpy as np
```

---

## 1️⃣ First Look (Always Do This)

```python
df.head()
df.info()
df.describe(include="all")
```

```python
df.shape
df.columns
```

---

## 2️⃣ Fix Column Names

### Standardize Column Names

```python
df.columns = df.columns.str.strip().str.lower().str.replace(" ", "_")
```

```python
df.columns = (
    df.columns
      .str.lower()
      .str.replace(r"[^\w]+", "_", regex=True)
)
```

---

## 3️⃣ Handle Missing Values

### Detect Missing Data

```python
df.isna().sum()
```

```python
df.isnull().mean() * 100  # percent missing
```

### Drop Missing Data

```python
df.dropna()
df.dropna(subset=["age", "salary"])
```

### Fill Missing Data

```python
df.fillna(0)
```

```python
df["age"] = df["age"].fillna(df["age"].median())
```

```python
df["city"] = df["city"].fillna("Unknown")
```

---

## 4️⃣ Fix Data Types

### Check Types

```python
df.dtypes
```

### Convert Types

```python
df["age"] = df["age"].astype(int)
```

```python
df["salary"] = pd.to_numeric(df["salary"], errors="coerce")
```

```python
df["date"] = pd.to_datetime(df["date"], errors="coerce")
```

---

## 5️⃣ Clean String Columns

### Strip Whitespace

```python
df["name"] = df["name"].str.strip()
```

### Case Normalization

```python
df["city"] = df["city"].str.lower()
```

```python
df["city"] = df["city"].str.title()
```

### Replace Values

```python
df["gender"] = df["gender"].replace({
    "M": "Male",
    "F": "Female",
    "male ": "Male"
})
```

### Remove Special Characters

```python
df["phone"] = df["phone"].str.replace(r"\D", "", regex=True)
```

---

## 6️⃣ Handle Duplicates

### Find Duplicates

```python
df.duplicated().sum()
```

```python
df[df.duplicated()]
```

### Remove Duplicates

```python
df.drop_duplicates()
```

```python
df.drop_duplicates(subset=["email"])
```

---

## 7️⃣ Fix Inconsistent Values

### Normalize Categories

```python
df["country"] = df["country"].replace({
    "USA": "US",
    "United States": "US",
    "U.S.": "US"
})
```

### Conditional Fixes

```python
df.loc[df["age"] < 0, "age"] = np.nan
```

```python
df.loc[df["salary"] < 0, "salary"] = 0
```

---

## 8️⃣ Outliers & Bad Data

### Clip Values

```python
df["salary"] = df["salary"].clip(lower=0, upper=200000)
```

### Remove Outliers (IQR)

```python
Q1 = df["salary"].quantile(0.25)
Q3 = df["salary"].quantile(0.75)
IQR = Q3 - Q1

df = df[(df["salary"] >= Q1 - 1.5 * IQR) &
        (df["salary"] <= Q3 + 1.5 * IQR)]
```

---

## 9️⃣ Create Cleaned Columns

### Conditional Columns

```python
df["is_adult"] = df["age"] >= 18
```

```python
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 17, 64, 120],
    labels=["child", "adult", "senior"]
)
```

---

## 🔟 Validate Data

### Check Ranges

```python
df["age"].between(0, 120).all()
```

### Check Uniqueness

```python
df["email"].is_unique
```

### Quick Sanity Checks

```python
df["country"].value_counts()
```

---

## 🧠 Cleaning Workflow (Memorize This)

```python
df = (
    df
    .rename(columns=str.lower)
    .assign(age=lambda x: x["age"].fillna(x["age"].median()))
    .drop_duplicates()
)
```

---

## ⚡ Golden Rules of Data Cleaning

* Fix **column names first**
* Convert **types early**
* Handle **missing values explicitly**
* Normalize **categories**
* Validate **after every major step**

---
Perfect! We can handle **leading and trailing spaces** in a single, clean **one-liner pandas solution**. Here’s the updated version:

```python
import pandas as pd

def clean_column_headers(df):
    """
    Cleans DataFrame column headers by:
    - Stripping leading/trailing spaces
    - Converting to lowercase
    - Removing special characters
    - Replacing multiple spaces with underscores
    - Stripping leading/trailing underscores
    """
    df.columns = (
        df.columns
        .str.strip()  # Remove leading/trailing spaces
        .str.lower()  # Convert to lowercase
        .str.replace(r'[^0-9a-zA-Z _]', '', regex=True)  # Remove special characters
        .str.replace(r'\s+', '_', regex=True)  # Replace spaces with underscores
        .str.strip('_')  # Remove leading/trailing underscores
    )
    return df

# Example usage
data = {
    ' Name!  ': ['Alice', 'Bob'],
    ' Age#': [25, 30],
    'E-mail@ Address ': ['alice@example.com', 'bob@example.com']
}

df = pd.DataFrame(data)
print("Before cleaning:")
print(df)

df = clean_column_headers(df)
print("\nAfter cleaning:")
print(df)
```

**Output:**

```
Before cleaning:
      Name!   Age#      E-mail@ Address 
0     Alice     25   alice@example.com
1       Bob     30     bob@example.com

After cleaning:
    name  age  email_address
0  Alice   25  alice@example.com
1    Bob   30    bob@example.com
```

---

✅ **What changed:**

* `.str.strip()` at the start removes leading/trailing spaces before any other processing.
* Everything else (lowercasing, removing special characters, replacing spaces, stripping underscores) stays vectorized and fast.

If you want, I can make an **even shorter one-liner** that does all of this in a single `.columns = ...` without multiple `.str` calls—still fully vectorized. This can be nice for super concise scripts.

Do you want me to do that?





