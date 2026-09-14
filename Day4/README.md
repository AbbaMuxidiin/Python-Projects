Student Enrollment Data Analysis

Project Overview

This project analyzes a Student Enrollment dataset using Python and Pandas. The notebook focuses mainly on exploring the dataset, identifying missing values, calculating missing-value percentages, and examining the most frequent values (mode) in each column.

The dataset contains 300 student enrollment records and 7 columns:

Student_ID

Gender

Program

Enrollment_Date

Study_Mode

Tuition_Fee

Enrollment_Status

The analysis was performed in a Google Colab/Jupyter Notebook using Python and Pandas.

Objectives

The main objectives of this project are to:

Load the enrollment dataset into Pandas.

Inspect the first records of the dataset.

Check the data types of all columns.

Identify missing values in each column.

Calculate the percentage of missing values.

Find the most frequent value (mode) for each column.

Explore the distribution of students across academic programs.

Support data-cleaning decisions before further analysis.

Dataset Structure

Column

Description

Student_ID

Unique identifier assigned to a student

Gender

Student gender

Program

Academic program

Enrollment_Date

Date the student enrolled

Study_Mode

Study mode, such as Full-Time or Online

Tuition_Fee

Student tuition fee

Enrollment_Status

Current enrollment status

Missing Value Analysis

The notebook identified missing values in every column.

Column

Missing Values

Missing Percentage

Student_ID

15

5.00%

Gender

15

5.00%

Program

16

5.33%

Enrollment_Date

17

5.67%

Study_Mode

19

6.33%

Tuition_Fee

15

5.00%

Enrollment_Status

18

6.00%

The highest missing-value percentage was found in Study_Mode at 6.33%.

The notebook used Pandas functions such as:

data.isnull().sum()

and:

missing_percentage = data.isnull().mean() * 100
print(missing_percentage)

Mode Analysis

The notebook calculated the most frequent value for each column.

Column

Mode

Count

Student_ID

ENR0026

2

Gender

Female

148

Program

Computer Science

73

Enrollment_Date

2025-11-26

4

Study_Mode

Full-Time

159

Tuition_Fee

998.42

2

Enrollment_Status

Active

174

For example, Female is the most frequent value in the Gender column, appearing 148 times.

Computer Science is the most frequent program, with 73 records, followed by Data Science with 65 records and Business Administration with 46 records.

Program Distribution

The notebook found the following program counts:

Program

Count

Computer Science

73

Data Science

65

Business Administration

46

Engineering

37

Public Health

35

Economics

25

Unknown

1

CS

1

BA

1

The results show that Computer Science has the largest number of enrollment records.

The presence of values such as CS, BA, and Unknown indicates that additional standardization may be useful during the data-cleaning stage.

Data Quality Observations

The analysis identified several data-quality issues:

Missing values exist across all seven columns.

Gender contains inconsistent capitalization, such as Male, MALE, and male.

Study_Mode contains variations such as Full-Time, Online, and part-time.

Enrollment_Status contains variations such as Graduated and graduated.

Program contains abbreviated values such as CS and BA, as well as Unknown.

All columns were initially detected as object data types in the notebook.

These issues should be standardized before performing final analysis or building dashboards.

Data Cleaning Approach

For categorical columns, the notebook explored using the mode to understand the most common value and potentially fill missing values.

Examples include:

Gender → Female

Program → Computer Science

Study_Mode → Full-Time

Enrollment_Status → Active

For missing values, another possible approach is to remove incomplete rows using:

data_clean = data.dropna()

However, dropna() removes an entire row when at least one value is missing. Therefore, the choice between removing rows and filling missing values should depend on the purpose of the analysis and the importance of preserving records.

Tools and Technologies

Python

Pandas

Google Colab / Jupyter Notebook

Microsoft Excel as the source data format

Key Findings

The dataset contains 300 student records.

There are 7 variables related to student enrollment.

Missing values range from 5.00% to 6.33% by column.

Study_Mode has the highest missing-value rate at 6.33%.

Female is the most frequent gender value with 148 records.

Computer Science is the most common program with 73 records.

Full-Time is the most common study mode with 159 records.

Active is the most common enrollment status with 174 records.

Program and categorical-value inconsistencies require further cleaning.

Conclusion

This project provides an initial data-quality and exploratory analysis of student enrollment information. The analysis successfully identifies missing values, measures their percentages, calculates common values, and highlights inconsistent categorical entries.

The cleaned dataset can be used as the foundation for further work, including exploratory data analysis, PivotTables, visualizations, KPIs, and an enrollment dashboard.

Author

Abba Muxidiin
