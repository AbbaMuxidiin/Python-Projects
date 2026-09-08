Student Enrollment Data — Pandas Practice Notebook

This notebook walks through core pandas operations for loading, cleaning, selecting, filtering, and sorting a student enrollment dataset (Project Excel.xlsx, 300 rows).

Dataset Columns
Column	Description
Student_ID	Unique student identifier (e.g. ENR0001)
Gender	Male / Female / non_gender (dirty values present)
Program	e.g. Computer Science, Data Science, Public Health, Business Administration, Economics, Engineering
Enrollment_Date	Date the student enrolled (some values are non_date)
Study_Mode	Full-Time / Part-Time / Online (some values are non_study_mode)
Tuition_Fee	Fee amount (some are 0.0)
Enrollment_Status	Active / Graduated / Withdrawn / Deferred (some are non_status)
Year, Monthly	Derived from enrollment date
Clean_Enrollment_Date	Cleaned version of Enrollment_Date
1. Setup
python
import pandas as pd

# Load data from Google Drive
data2 = pd.read_excel("/content/drive/MyDrive/Colab Notebooks/python/Project Excel.xlsx")
2. Data Cleaning / Column Selection

Select one column:

python
data2['Gender']

Select multiple columns:

python
data2[['Program', 'Study_Mode', 'Tuition_Fee']]
3. Row Selection

Single row by position (iloc):

python
data2.iloc[299]
data2.iloc[0]

Multiple rows by position:

python
data2.iloc[1:10]
data2.iloc[5:10]

Row selection by label (loc):

python
data2.loc[1:10]

Rows + specific columns (loc):

python
data2.loc[10:100, ['Gender', 'Program']]

Rows + columns by position (iloc):

python
data2.iloc[5:10, 3:7]

Tip: iloc uses integer positions (end-exclusive), while loc uses labels (end-inclusive).

4. Filtering Data

Numerical / equality filter:

python
data2[data2['Program'] == 'Computer Science']

Filter using multiple category values (isin):

python
data2[data2['Gender'].isin(['Female', 'NaN'])]

Multiple conditions combined (&):

python
data2[
    (data2['Gender'] == 'Female') &
    (data2['Program'] == 'Computer Science') &
    (data2['Enrollment_Status'] == 'Graduated')
]
5. Sorting Data

Ascending:

python
data2.sort_values('Gender', ascending=True)

Descending:

python
data2.sort_values('Gender', ascending=False)
Key Takeaways
iloc → position-based selection (integers, end-exclusive).
loc → label-based selection (can use column names, end-inclusive).
Boolean masks (df[condition]) are used for filtering; combine conditions with & (and) or | (or), wrapping each condition in parentheses.
.isin([...]) is useful for filtering against a list of possible values.
.sort_values(column, ascending=True/False) sorts rows by a column.
The dataset contains intentional "dirty" values (non_status, non_date, non_program, non_gender, non_study_mode, 0.0 fees) meant to be handled during data cleaning.
