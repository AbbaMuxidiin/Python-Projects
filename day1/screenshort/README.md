# Student Enrollment Data Analysis Using Pandas

A Jupyter/Colab notebook project that explores, cleans, and analyzes a student enrollment dataset (`Excel_Project_Datasets_23_Assigned_Students...Enrollment.xlsx`) using the **pandas** library in Python.

## 📁 Dataset

- **Source file:** Google Drive (`/content/drive/MyDrive/Colab Notebooks/python/...xlsx`)
- **Sheet used:** `01_Enrollment`
- **Shape:** 300 rows × 9 columns

### Columns
| Column | Description |
|---|---|
| `Student_ID` | Unique student identifier (e.g. `ENR0001`) |
| `Gender` | Male / Female / non_gender (dirty values present) |
| `Program` | Field of study (Computer Science, Data Science, Public Health, Business Administration, Economics, Engineering, etc.) |
| `Enrollment_Date` | Date the student enrolled |
| `Study_Mode` | Full-Time / Part-Time / Online (some dirty values like `non_stady_mode`) |
| `Tuition_Fee` | Tuition amount |
| `Enrollment_Status` | Active / Graduated / Withdrawn / Deferred (some dirty values like `non_status`) |
| `Unnamed: 7` / `Unnamed: 8` | Extra blank/junk columns from the raw file |

> ⚠️ The raw dataset intentionally contains missing values and "dirty" placeholder text (e.g. `non_date`, `non_status`, `non_gender`, `non_program`) to practice data cleaning.

## 🎯 Project Goals

This notebook walks through a typical pandas data-analysis workflow:

1. **Load the dataset** from Google Drive using `pd.read_excel()`
2. **Explore the data**
   - `data.head()`, `data.tail()`, `data.sample(5)`
   - `data.shape` → check number of rows/columns
   - `data.columns` → list column names
   - `data.dtypes` → check data types
   - `data.info()` → summary of non-null counts and dtypes
   - `data.describe(include="all")` → statistical summary
3. **Data cleaning**
   - Handling missing/blank columns (`Unnamed: 7`, `Unnamed: 8`)
   - Fixing placeholder/dirty values (`non_status`, `non_gender`, `non_date`, etc.)
   - Creating a cleaned date column (`Clean_Enrollment_Date`)
   - Deriving `Year` and `Monthly` columns from `Enrollment_Date`
4. **Selecting data**
   - Single column: `data2['Gender']`
   - Multiple columns: `data2[['Program', 'Study_Mode', 'Tuition_Fee']]`
5. **Selecting rows with `iloc`**
   - Single row: `data2.iloc[299]`
   - Multiple rows: `data2.iloc[1:10]`
   - Row + column slicing: `data2.iloc[5:10, 3:7]`
6. **Selecting rows/columns with `loc`**
   - `data2.loc[1:10]`
   - `data2.loc[10:100, ['Gender', 'Program']]`
7. **Filtering data**
   - Single condition: `data2[data2['Program'] == 'Computer Science']`
   - Multiple categories: `data2[data2['Gender'].isin(['Female', 'NaN'])]`
   - Multiple conditions (AND logic):
     ```python
     data2[
         (data2['Gender'] == 'Female') &
         (data2['Program'] == 'Computer Science') &
         (data2['Enrollment_Status'] == 'Graduated')
     ]
     ```
8. **Sorting data**
   - `data2.sort_values('Gender', ascending=True)`
   - `data2.sort_values('Gender', ascending=False)`

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
3. Update the file path in the `pd.read_excel()` call to match your Drive location.
4. Run the cells in order — starting with **Load Dataset**, then **Data Exploration**, **Data Cleaning**, **Sorting and Filtering**.

## 📌 Notes

- `data1` refers to the raw/original DataFrame; `data2` refers to the cleaned working DataFrame used for selection, filtering, and sorting exercises.
- This project is primarily a **learning/practice notebook** for core pandas operations: exploration, selection (`iloc`/`loc`), filtering, and sorting.
