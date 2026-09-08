# Student Enrollment Data Cleaning with Pandas

A Jupyter/Colab notebook project focused on **cleaning inconsistent categorical data** in a student enrollment dataset using **pandas**.

## 📁 Dataset

- **Source file:** Google Drive (`/content/drive/MyDrive/Colab Notebooks/Enrollment_python.xlsx`)
- **Loaded with:** `pd.read_excel()`
- **Shape:** 300 rows × 7 columns

### Columns
| Column | Description |
|---|---|
| `Student_ID` | Unique student identifier (e.g. `ENR0123`) |
| `Gender` | Male / Female (contains inconsistent casing/typos) |
| `Program` | Field of study (Computer Science, Data Science, Business Administration, Engineering, Public Health, Economics, plus a few messy entries) |
| `Enrollment_Date` | Date the student enrolled |
| `Study_Mode` | Full-Time / Part-Time / Online |
| `Tuition_Fee` | Tuition amount (loaded as text/object, needs conversion to numeric) |
| `Enrollment_Status` | Active / Graduated / Deferred / Withdrawn (contains inconsistent casing) |

## 🎯 Project Goals

This notebook demonstrates a real-world **data cleaning workflow**:

1. **Load the data**
   ```python
   import pandas as pd
   data = pd.read_excel("/content/drive/MyDrive/Colab Notebooks/Enrollment_python.xlsx")
   data.head()
   ```

2. **Inspect data types**
   - `data.dtypes` → confirm all columns are loaded as `object` (text)

3. **Find inconsistent / dirty categories with `value_counts()`**
   - `data['Program'].value_counts()` revealed messy entries like `"CS"`, `"BA"`, and `"Unknown"` mixed in with the clean program names.
   - `data['Gender'].value_counts()` revealed inconsistent entries like `"male"`, `"MALE"`, and a stray `"-"` alongside `"Male"` / `"Female"`.
   - `data['Enrollment_Status'].value_counts()` revealed inconsistent casing such as `"ACTIVE"`, `"graduated"`, and `"deferred"`.

4. **Standardize categories with `.replace()`**
   ```python
   # Program
   data['Program'] = data['Program'].replace("CS", "Computer Science")
   data['Program'] = data['Program'].replace("BA", "Business Administration")

   # Gender
   data['Gender'] = data['Gender'].replace("MALE", "Male")
   data['Gender'] = data['Gender'].replace("male", "Male")

   # Enrollment_Status
   data['Enrollment_Status'] = data['Enrollment_Status'].replace("ACTIVE", "Active")
   data['Enrollment_Status'] = data['Enrollment_Status'].replace("graduated", "Graduated")
   data['Enrollment_Status'] = data['Enrollment_Status'].replace("deferred", "Deferred")
   ```
   After each replacement, `value_counts()` is re-run to confirm the fix and spot any remaining inconsistencies (e.g. the leftover `"-"` entry in `Gender`, and `"Unknown"` in `Program`).

5. **Rename columns**
   ```python
   data.rename(columns={"Student_ID": "STD"})
   ```

6. **Convert `Tuition_Fee` to numeric**
   - Directly casting with `.astype(float)` fails because of a stray `"-"` value:
     ```python
     data['Tuition_Fee'] = data['Tuition_Fee'].astype(float)
     # ValueError: could not convert string to float: '-'
     ```
   - Fixed using `pd.to_numeric()` with `errors="coerce"`, which safely converts invalid entries to `NaN` instead of raising an error:
     ```python
     data['Tuition_Fee'] = pd.to_numeric(data['Tuition_Fee'], errors="coerce")
     ```

## 🛠️ Tools & Libraries

- Python 3
- [pandas](https://pandas.pydata.org/)
- Google Colab (with Google Drive mounted for file access)

## ▶️ How to Run

1. Open the notebook in **Google Colab**.
2. Mount your Google Drive:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
3. Update the file path in `pd.read_excel()` to match your Drive location.
4. Run the cells top to bottom — the notebook checks each column's unique values with `value_counts()`, cleans inconsistent text with `.replace()`, and converts `Tuition_Fee` to numeric with `pd.to_numeric(..., errors="coerce")`.

## 📌 Key Takeaways

- Always inspect categorical columns with `value_counts()` before analysis — mixed casing and typos (`MALE`, `male`, `-`) are common in real data.
- `.replace()` is a simple way to standardize known bad values one at a time.
- Prefer `pd.to_numeric(col, errors="coerce")` over `.astype(float)` when a column may contain non-numeric junk — it converts what it can and turns the rest into `NaN` instead of crashing.

