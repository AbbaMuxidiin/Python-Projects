


Day 2 – Pandas Data Selection, Filtering & Sorting
Overview
This notebook is a practical introduction to working with tabular data using Python and Pandas. The exercises use a student enrollment dataset loaded from an Excel file and demonstrate how to select columns and rows, filter records using conditions, and sort data.

The notebook contains examples of:

Importing Pandas

Reading Excel data

Selecting single and multiple columns

Selecting rows with iloc

Selecting rows and columns with loc

Filtering data using conditions

Filtering multiple categories with isin()

Applying multiple conditions with &

Sorting data in ascending and descending order

Technologies Used
Python 3

Pandas

Google Colab

Microsoft Excel / .xlsx dataset

Dataset
The notebook works with a student enrollment dataset containing fields such as:

Column	Description
Student_ID	Unique student identifier
Gender	Student gender
Program	Academic program
Enrollment_Date	Student enrollment date
Study_Mode	Study mode
Tuition_Fee	Tuition fee
Enrollment_Status	Current enrollment status
Year	Enrollment year
Monthly	Enrollment month
Clean_Enrollment_Date	Cleaned enrollment date
The notebook loads the Excel dataset using Pandas read_excel().

Notebook Structure
1. Import Pandas
The notebook starts by importing Pandas:

import pandas as pd
Pandas provides the main tools used throughout the exercises for working with DataFrames.

2. Read Excel Data
The dataset is loaded into a DataFrame:

data2 = pd.read_excel("/content/drive/MyDrive/Colab Notebooks/python/Project Excel.xlsx")
The DataFrame is stored in the variable data2.

3. Selecting a Single Column
A single column can be selected using its column name:

data2['Gender']
This returns the Gender column from the dataset.

4. Selecting Multiple Columns
Multiple columns can be selected by passing a list of column names:

data2[['Program', 'Study_Mode', 'Tuition_Fee']]
This example selects:

Program

Study_Mode

Tuition_Fee

5. Selecting Rows with iloc
iloc is used for selecting data based on integer positions.

Select one row:

data2.iloc[299]
Select multiple rows:

data2.iloc[1:10]
The notebook also demonstrates selecting a range of rows and columns:

data2.iloc[5:10, 3:7]
6. Selecting Data with loc
loc is used for selecting data based on labels/index values.

Select a range of rows:

data2.loc[1:10]
Select specific rows and columns:

data2.loc[10:100, ['Gender', 'Program']]
7. Filtering Data
Filtering allows us to return only records that meet a specific condition.

For example, selecting students enrolled in Computer Science:

data2[data2['Program'] == 'Computer Science']
The notebook demonstrates that this filter returns 74 rows from the dataset.

8. Filtering Multiple Categories
The isin() function can be used when filtering for multiple possible values:

data2[data2['Gender'].isin(['Female', 'NaN'])]
This is useful when a column needs to be compared against more than one category.

9. Multiple Conditions
Multiple conditions can be combined using the & operator:

data2[
    (data2['Gender'] == 'Female') &
    (data2['Program'] == 'Computer Science') &
    (data2['Enrollment_Status'] == 'Graduated')
]
This allows the dataset to be filtered using several requirements at the same time.

10. Sorting Data
The sort_values() function is used to sort records.

Ascending order:

data2.sort_values('Gender', ascending=True)
Descending order:

data2.sort_values('Gender', ascending=False)
Key Pandas Concepts Learned
Concept	Purpose
pd.read_excel()	Load Excel data into Pandas
data2['Column']	Select one column
data2[['A', 'B']]	Select multiple columns
iloc[]	Select by integer position
loc[]	Select by label/index
isin()	Filter multiple category values
Boolean conditions	Filter records
&	Combine multiple conditions
sort_values()	Sort DataFrame values
Learning Objectives
By completing this notebook, you should be able to:

Load Excel data into a Pandas DataFrame.

Select individual columns.

Select multiple columns.

Select individual rows using iloc.

Select multiple rows using iloc.

Select rows and columns using loc.

Filter data using comparison conditions.

Filter records using multiple categories.

Combine multiple filtering conditions.

Sort a DataFrame in ascending or descending order.

Example Workflow
A typical Pandas workflow from this notebook is:

import pandas as pd

# Load dataset
data2 = pd.read_excel("Project Excel.xlsx")

# Select columns
data2[['Program', 'Study_Mode', 'Tuition_Fee']]

# Filter records
data2[data2['Program'] == 'Computer Science']

# Apply multiple conditions
data2[
    (data2['Gender'] == 'Female') &
    (data2['Program'] == 'Computer Science') &
    (data2['Enrollment_Status'] == 'Graduated')
]

# Sort data
data2.sort_values('Gender', ascending=True)
Project Focus
This Day 2 notebook focuses on the fundamentals of Pandas DataFrame selection, filtering, and sorting using a student enrollment dataset. It is intended as a hands-on learning exercise for beginners working toward data analysis with Python.

File
Day2.ipynb – Jupyter/Google Colab notebook containing the exercises and examples.

Author
Abba Muxidiin
