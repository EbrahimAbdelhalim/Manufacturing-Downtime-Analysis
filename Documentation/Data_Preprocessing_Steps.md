Power BI Data Preparation & Preprocessing Documentation
This document describes the data preparation and preprocessing steps performed using Power Query and DAX during the development of the Production Performance Dashboard project.

Dim_Downtime_Factors Table

1.	Removed duplicate rows to ensure unique downtime factors.
2.	Replaced Yes/No values with TRUE/FALSE in the 'Operator Error' column.
3.	Changed the data type of 'Operator Error' from Text to Boolean.
4.	Added a custom column named 'Is Human' to classify downtime as Human or System.

Dim_Downtime Table

5.	Applied Unpivot Columns transformation to normalize downtime factor columns.
6.	Renamed columns for better readability and consistency.

Fact_Production Table

7.	Changed all columns to their appropriate data types.
8.	Removed duplicate records.
9.	Added a custom column named 'Actual Batch Time' using the formula:

Duration.TotalMinutes([End Time] - [Start Time]).

10.	Changed the 'Actual Batch Time' column data type to Whole Number.
11.	Merged queries with the Dim_Products table to retrieve the 'Min Batch Time' column.
12.	Added a custom column named 'Batches Type' to classify batches as Delayed or On_Time, then converted the column type to Text.

Dim_Products Table

13.	Removed duplicate rows.
14.	Changed all columns to their appropriate data types.

Date Table & DAX Calculations

15.	Created a Dim_Date table using the CALENDAR function.
16.	Created a Day column using DAY(Dim_Date[Date]).
17.	Created a Month column using MONTH(Dim_Date[Date]).
18.	Created a Month Name column using FORMAT(Dim_Date[Date], "mmm").
19.	Created a Week column using WEEKNUM(Dim_Date[Date],2).
20.	Created a Year column using YEAR(Dim_Date[Date]).

DAX Code Snippets

Dim_Date = CALENDAR(MIN('Fact_Production'[Date]),MAX('Fact_Production'[Date]))
Day = DAY(Dim_Date[Date])
Month = MONTH(Dim_Date[Date])
Month Name = FORMAT(Dim_Date[Date],"mmm")
Week = WEEKNUM(Dim_Date[Date],2)
Year = YEAR(Dim_Date[Date])

These preprocessing and transformation steps ensured data consistency, improved data quality, and enabled accurate KPI calculations and dashboard visualizations.
