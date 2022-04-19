# Fundamentals of data analysis in pandas

This is a cheat sheet for the most useful commands used for data analysis in pandas.

<!-- TOC -->

- [Fundamentals of data analysis in pandas](#fundamentals-of-data-analysis-in-pandas)
  - [Importing data](#importing-data)
    - [Importing most common libraries](#importing-most-common-libraries)
    - [Importing a CSV file](#importing-a-csv-file)
    - [Importing an Excel file](#importing-an-excel-file)
    - [Importing files correctly: delimiters and dates](#importing-files-correctly-delimiters-and-dates)
  - [First steps after importing - best practice](#first-steps-after-importing---best-practice)
    - [Check the data types of each column](#check-the-data-types-of-each-column)
    - [Converting columns to datetime](#converting-columns-to-datetime)
  - [Quick data overview: Exploratory analysis](#quick-data-overview-exploratory-analysis)
    - [Get all of the unique values from a given column, along with a count for each value](#get-all-of-the-unique-values-from-a-given-column-along-with-a-count-for-each-value)
  - [Exporting data](#exporting-data)
    - [Exporting to a CSV file](#exporting-to-a-csv-file)
    - [Exporting to an Excel file](#exporting-to-an-excel-file)
  - [Sorting Data](#sorting-data)
    - [Sort by given column](#sort-by-given-column)

<!-- /TOC -->

## Importing data

### Importing most common libraries

```python
import pandas as pd
import numpy as np
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
```

### Importing a CSV file

```python
# File is being imported from the "data" folder.
df = pd.read_csv("data/filename.csv")
```

### Importing an Excel file

```python
# File is being imported from the "data" folder.
df = pd.read_excel("data/filename.xlsx")
```

### Importing files correctly: delimiters and dates

```python
pd.read_csv("data/file.csv", sep=';', parse_dates=["Date"])
```

> This will import `file.csv`, delimiting columns based on a semicolon, and will make sure that the "Date" column is imported with a data type of "datetime", as opposed to "object". (Note that this will throw an error if pandas finds any data points which it cannot parse correctly.)

## First steps after importing - best practice

### Check the data types of each column

```python
df.dtypes
# COUNTRY     object
# POP        float64
# AREA       float64
# GDP        float64
# CONT        object
# IND_DAY     object
# dtype: object
```

### Converting columns to datetime

```python
sales["Calculated_Date"] = pd.to_datetime(sales["Calculated_Date"])
```

## Quick data overview: Exploratory analysis

### Get all of the unique values from a given column, along with a count for each value

```python
# Optional parameters included for assistance
df["column_name"].value_counts(normalize=False, sort=True, ascending=False, bins=None, dropna=True)
```

## Exporting data

### Exporting to a CSV file

```python
# File is being imported from the "data" folder.
df.to_csv("data.csv")
```

### Exporting to an Excel file

```python
# File is being imported from the "data" folder.
df.to_excel("data.xlsx")
```

## Sorting Data

### Sort by given column

```python
# We are sorting the sales dataframe by revenue, descending.
sales.sort_values(["Revenue"], ascending=False).head(5)
```
