# Student Enrollment Data Analysis Using Python

## Overview

This project explores a student enrollment dataset using Python and pandas in Google Colab. It focuses on inspecting data types, identifying missing values, calculating missing percentages, and finding the most frequent values in each column.

The results documented here are based on the supplied notebook screenshots. The original Excel workbook was not independently checked.

## Objectives

- Load student enrollment data from Excel.
- Preview the dataset and inspect column data types.
- Calculate missing values and percentages.
- Identify the mode and its frequency.
- Explore program enrollment counts.
- Identify data quality issues for further cleaning.

## Tools Used

- Python
- pandas
- openpyxl
- Google Colab

## Dataset

**File:** `Enrollment_python - 2.xlsx`

The screenshots show **300 rows and 7 columns**.

| Column | Description |
| --- | --- |
| Student_ID | Student identifier |
| Gender | Recorded student gender |
| Program | Academic program |
| Enrollment_Date | Date of enrollment |
| Study_Mode | Learning format |
| Tuition_Fee | Recorded tuition fee |
| Enrollment_Status | Student enrollment status |

All seven columns initially appear with the `object` data type.

## Getting Started

Install the required libraries in a notebook cell if needed:

```python
%pip install pandas openpyxl
```

For Google Colab, mount Google Drive:

```python
from google.colab import drive

drive.mount("/content/drive")
```

Load the workbook. Update the path to match your file location:

```python
import pandas as pd

file_path = "/content/drive/MyDrive/Colab Notebooks/Enrollment_python - 2.xlsx"
data = pd.read_excel(file_path)
```

Run the following sections in order.

## 1. Inspect the Dataset

```python
data.head()
```

Display the first five rows.

```python
data.shape
```

Check the number of rows and columns.

```python
data.dtypes
```

Inspect the data type of each column.

## 2. Identify Missing Values

Check individual values in the Gender column:

```python
data["Gender"].isnull()
```

`True` indicates a missing value. `False` indicates a non-missing value.

Create a summary table for all columns:

```python
missing_summary = pd.DataFrame({
    "Missing_Count": data.isnull().sum(),
    "Missing_Percentage": data.isnull().mean() * 100
})

missing_summary = missing_summary.round(2)
missing_summary
```

### Reported Results

| Column | Missing Count | Missing Percentage |
| --- | ---: | ---: |
| Student_ID | 15 | 5.00% |
| Gender | 15 | 5.00% |
| Program | 16 | 5.33% |
| Enrollment_Date | 17 | 5.67% |
| Study_Mode | 19 | 6.33% |
| Tuition_Fee | 15 | 5.00% |
| Enrollment_Status | 18 | 6.00% |

There are **115 missing cells** out of **2,100 total cells**, equivalent to **5.48%**.

This is the number of missing cells, not the number of rows containing missing values.

`Study_Mode` has the highest missing percentage at **6.33%**.

## 3. Calculate the Mode

The mode is the most frequently occurring non-missing value.

Example for Gender:

```python
gender_modes = data["Gender"].mode()

if not gender_modes.empty:
    gender_mode = gender_modes.iloc[0]
    gender_count = data["Gender"].value_counts()[gender_mode]

    print("Column:", "Gender")
    print("Mode:", gender_mode)
    print("Count:", gender_count)
```

Reported output:

```text
Column: Gender
Mode: Female
Count: 148
```

### Mode Results Shown in the Notebook

| Column | Displayed Mode | Count |
| --- | --- | ---: |
| Student_ID | ENR0026 | 2 |
| Gender | Female | 148 |
| Program | Computer Science | 73 |
| Enrollment_Date | 2025-11-26 00:00:00 | 4 |
| Study_Mode | Full-Time | 159 |
| Tuition_Fee | 998.42 | 2 |
| Enrollment_Status | Active | 174 |

The original code selects one mode using `.mode()[0]`. A column can have multiple values tied for the highest frequency.

The notebook also shows a mixed-type sorting warning, so the displayed modes should be reviewed after data types are cleaned.

### Create a Table Including Tied Modes

This version avoids sorting mixed data values and handles columns with no non-missing values:

```python
results = []

for column in data.columns:
    counts = data[column].value_counts(dropna=True, sort=False)

    if counts.empty:
        modes = []
        count = 0
    else:
        count = int(counts.max())
        modes = counts[counts == count].index.tolist()

    results.append({
        "Column": column,
        "Mode_Values": modes,
        "Count": count
    })

mode_table = pd.DataFrame(results)
mode_table
```

## 4. Analyze Program Enrollment

```python
data["Program"].value_counts()
```

### Reported Results

| Program | Count |
| --- | ---: |
| Computer Science | 73 |
| Data Science | 65 |
| Business Administration | 46 |
| Engineering | 37 |
| Public Health | 35 |
| Economics | 25 |
| Unknown | 1 |
| CS | 1 |
| BA | 1 |

These counts total **284 non-missing program entries**. The remaining **16 entries** are missing.

`value_counts()` excludes missing values by default. To include them:

```python
data["Program"].value_counts(dropna=False)
```

Computer Science is the most frequent recorded program, with **73 entries**, before any category standardization.

## 5. Important Code Correction

The following assignment overwrites the original DataFrame:

```python
data = data.isna().mean() * 100
```

After this runs, `data` contains a Series of percentages rather than the enrollment records. Checking missing values again can therefore return `0.0`, because the percentage values themselves are not missing.

Keep the original DataFrame and use a separate variable:

```python
missing_percentage = data.isnull().mean() * 100
print(missing_percentage)
```

If `data` has already been overwritten, reload the workbook first:

```python
data = pd.read_excel(file_path)
```

Also, this expression returns a proportion:

```python
data["Gender"].isnull().mean()
```

For Gender, `0.05` means **5%**. Multiply by 100 to express it as a percentage.

## Data Quality Issues and Next Steps

The screenshots demonstrate inspection and analysis; they do not show a completed cleaning process.

- Review missing values before deciding whether to fill or remove them.
- Review `Unknown`, which is a text value and is not counted as missing by `isnull()`.
- Confirm whether `CS` means Computer Science and `BA` means Business Administration before combining categories.
- Validate and convert `Enrollment_Date` to a datetime type.
- Validate and convert `Tuition_Fee` to a numeric type.
- Investigate repeated student IDs. A repeated ID does not necessarily mean an entire row is duplicated.
- Recalculate all summaries after cleaning.

## Key Findings

- The dataset contains 300 rows and 7 columns.
- There are 115 missing cells, representing 5.48% of all cells.
- Study_Mode has the highest missing-value count: 19.
- Female is the most frequent Gender value: 148.
- Computer Science is the most frequent Program value: 73.
- Full-Time is the most frequent Study_Mode value: 159.
- Active is the most frequent Enrollment_Status value: 174.
- Missing values, inconsistent labels, and mixed data types require further review.
