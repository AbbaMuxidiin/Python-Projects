# Day 1 – Introduction to Pandas and Dataset Exploration

## Overview

This notebook is **Day 1** of a Python Data Analysis learning series. It introduces the basics of **Pandas** and demonstrates how to load, inspect, and understand datasets using Python.

The main focus of this notebook is **exploratory dataset inspection** before performing data cleaning or analysis.

## Objectives

By completing this notebook, you will learn how to:

* Import the Pandas library
* Load Excel datasets into Python
* Display the first rows of a dataset
* Display the last rows of a dataset
* Select random samples from a dataset
* Check the shape of a dataset
* Display column names
* Check data types
* Get general information about a dataset
* Generate descriptive statistics

## Technologies Used

* Python
* Pandas
* Google Colab
* Microsoft Excel (`.xlsx`)

## Import Pandas

The notebook begins by importing the Pandas library:

```python
import pandas as pd
```

Pandas is used to work with structured and tabular data in Python.

## Loading the Dataset

The notebook uses `pd.read_excel()` to load Excel files into a Pandas DataFrame.

Example:

```python
data = pd.read_excel("Excel_Project_Datasets_23_Assigned_Students_MORE_BLANKS_Abba_Muxidiin_Enrollment2222233344.xlsx")
```

Another dataset is also loaded for practice:

```python
data1 = pd.read_excel("test.xlsx")
```

And:

```python
data2 = pd.read_excel("Project Excel.xlsx")
```

## Dataset Exploration

### 1. Display the First Rows

The `head()` function displays the first rows of the dataset.

```python
data.head()
```

Example:

```python
data1.head()
```

This is useful for quickly checking what the dataset looks like.

### 2. Display the Last Rows

The `tail()` function displays the last rows of the dataset.

```python
data1.tail()
```

This helps verify the end of the dataset and inspect the final records.

### 3. Display Random Rows

The `sample()` function selects random rows from the dataset.

```python
data1.sample(5)
```

This is useful when you want to inspect random records rather than only the beginning or end of the dataset.

## Dataset Shape

The `shape` property shows the number of rows and columns.

```python
data1.shape
```

The notebook identifies the dataset as having:

* **300 rows**
* **9 columns**

The result is represented as:

```text
(300, 9)
```

## Display Column Names

The `columns` property displays all column names in the dataset.

```python
data1.columns
```

This helps identify the variables available for future analysis.

## Data Types

The `dtypes` property shows the data type of each column.

```python
data1.dtypes
```

Understanding data types is important before performing operations such as:

* Date analysis
* Numerical calculations
* Text processing
* Data cleaning

## Dataset Information

The `info()` function provides general information about the DataFrame.

```python
data1.info()
```

It can be used to inspect:

* Number of entries
* Column names
* Non-null values
* Data types
* Memory usage

## Descriptive Statistics

The `describe()` function generates descriptive statistics for numerical columns.

```python
data2.describe()
```

The notebook also demonstrates:

```python
data2.describe(include="all")
```

Using `include="all"` allows a broader summary of the columns, including non-numerical data where supported.

## Key Pandas Functions and Properties

| Function / Property | Purpose                         |
| ------------------- | ------------------------------- |
| `pd.read_excel()`   | Load an Excel file              |
| `head()`            | Display the first rows          |
| `tail()`            | Display the last rows           |
| `sample()`          | Display random rows             |
| `shape`             | Show rows and columns           |
| `columns`           | Show column names               |
| `dtypes`            | Show data types                 |
| `info()`            | Show DataFrame information      |
| `describe()`        | Generate descriptive statistics |

## Learning Workflow

The notebook follows this basic data-analysis workflow:

```text
Load Dataset
     ↓
View the Data
     ↓
Check Dataset Shape
     ↓
Check Columns
     ↓
Check Data Types
     ↓
Check Dataset Information
     ↓
Generate Descriptive Statistics
```

## Why Dataset Exploration Is Important

Before cleaning or analyzing data, it is important to understand the structure and content of the dataset.

Initial exploration helps identify:

* How large the dataset is
* What columns are available
* What types of data are present
* Whether values may be missing
* Whether numerical columns contain useful statistics
* How the dataset is structured

## Project Files

* `Day1.ipynb` – Jupyter/Google Colab notebook containing the Day 1 Pandas exercises.
* Excel datasets – Source files used for practicing dataset exploration.

## Conclusion

Day 1 provides the foundation for working with datasets using Pandas. The skills learned in this notebook are essential for the next stages of data analysis, including **data cleaning, filtering, transformation, visualization, and exploratory data analysis (EDA)**.

## Author

**Abba Muxidiin**

---

*Day 1 – Python Data Analysis with Pandas*

