# Python Data Analysis & Visualization Masterclass 2022 - Colt Steele

One-page summary of my notes from the course.

<!-- TOC -->

- [Python Data Analysis & Visualization Masterclass 2022 - Colt Steele](#python-data-analysis--visualization-masterclass-2022---colt-steele)
- [Section 4: Dataframes & datasets](#section-4-dataframes--datasets)
  - [Quick exploratory analysis](#quick-exploratory-analysis)
    - [Retrieving number of rows and columns](#retrieving-number-of-rows-and-columns)
    - [Quick overview of all data](#quick-overview-of-all-data)
    - [Quick overview of datatypes only](#quick-overview-of-datatypes-only)
  - [pandas reconfiguration](#pandas-reconfiguration)
  - [Headers](#headers)
    - [Overriding default headers](#overriding-default-headers)
- [Section 5: Basic Dataframe computations](#section-5-basic-dataframe-computations)
  - [`.sum()` & `.count()`](#sum--count)
    - [Using `.count()`](#using-count)
    - [Common `sum()` arguments](#common-sum-arguments)
  - [Mean, median, mode](#mean-median-mode)
  - [`.describe()`](#describe)
- [Section 6: Series & Columns](#section-6-series--columns)
  - [Important series methods](#important-series-methods)
  - [Ranking by one column](#ranking-by-one-column)
  - [Selecting multiple columns](#selecting-multiple-columns)
  - [Fundamentals of `value_counts()`](#fundamentals-of-value_counts)
  - [Combining `.plot()` with `.value_counts()` to create a quick plot](#combining-plot-with-value_counts-to-create-a-quick-plot)
- [Section 7: Indexing & Sorting](#section-7-indexing--sorting)
  - [Changing the index of a dataframe after importing](#changing-the-index-of-a-dataframe-after-importing)
  - [Changing the index of a dataframe when importing](#changing-the-index-of-a-dataframe-when-importing)
  - [Sorting by values](#sorting-by-values)
    - [Sorting by one column](#sorting-by-one-column)
    - [Sorting by multiple columns](#sorting-by-multiple-columns)
  - [Sorting by index](#sorting-by-index)
  - [Combining sorting and plotting](#combining-sorting-and-plotting)
  - [Returning data by rows](#returning-data-by-rows)
    - [`.loc` - by row label](#loc---by-row-label)
    - [`.iloc` - by row position (_integer_ label)](#iloc---by-row-position-integer-label)
    - [loc & iloc with specific columns](#loc--iloc-with-specific-columns)
- [Section 8: Filtering Dataframes](#section-8-filtering-dataframes)
  - [Filtering dataframes with a boolean series](#filtering-dataframes-with-a-boolean-series)
  - [Filtering with comparison operators](#filtering-with-comparison-operators)
  - [The `between` method](#the-between-method)
  - [The `isin()` method](#the-isin-method)
  - [Combining conditions using AND (&)](#combining-conditions-using-and-)
  - [Combining conditions using OR (|)](#combining-conditions-using-or-)
  - [Bitwise negation](#bitwise-negation)
  - [Filtering by missing values: `isna` and `notna` methods](#filtering-by-missing-values-isna-and-notna-methods)
- [Section 9: Adding & Removing columns](#section-9-adding--removing-columns)
  - [Dropping values](#dropping-values)
  - [Adding static columns](#adding-static-columns)
  - [Adding dynamic columns](#adding-dynamic-columns)
    - [Summing columns](#summing-columns)
    - [Calculating new values for columns](#calculating-new-values-for-columns)
- [Section 11: Working with Types and NA values](#section-11-working-with-types-and-na-values)
  - [Casting types with `astype()`](#casting-types-with-astype)
  - [Introducing the Category type](#introducing-the-category-type)
  - [Casting with pd.to_numeric()](#casting-with-pdto_numeric)
  - [dropna() and isna()](#dropna-and-isna)
    - [Dropping na values on a series](#dropping-na-values-on-a-series)
    - [Dropping na values on a dataframe](#dropping-na-values-on-a-dataframe)
  - [`fillna` - Replacing na values with another value](#fillna---replacing-na-values-with-another-value)
- [Section 12: Working with Dates & Times](#section-12-working-with-dates--times)
  - [Converting with pd.to_datetime()](#converting-with-pdto_datetime)
  - [Specifying date formats](#specifying-date-formats)
  - [Converting columns to datetimes](#converting-columns-to-datetimes)
  - [Useful `dt` properties](#useful-dt-properties)
  - [Comparing Dates](#comparing-dates)
  - [Date math & Timedeltas](#date-math--timedeltas)
- [Section 13: Matplotlib](#section-13-matplotlib)

<!-- /TOC -->

# Section 4: Dataframes & datasets

## Quick exploratory analysis

### Retrieving number of rows and columns

```python
df.shape
```

### Quick overview of all data

```python
df.info()
```

### Quick overview of datatypes only

```python
df.dtypes
```

## pandas reconfiguration

If you want to force-reconfigure pandas to display 15 rows at a time:

```python
pd.options.display.min_rows = 15
```

## Headers

### Overriding default headers

If there is no header data, you can provide it with the `names=` argument. Also, set `header=` to zero.

```python
names = ['sumlev', 'region', 'division', 'state', 'name', 'census2010pop',
'estimatesbase2010', 'popestimate2010', 'popestimate2011',
'popestimate2012', 'popestimate2013', 'popestimate2014',
'popestimate2015', 'popestimate2016', 'popestimate2017',
'popestimate2018', 'popestimate2019', 'popestimate042020', 'popestimate2020']
state_pops = pd.read_csv("data/nst-est2020.csv", names=names, header=0)
state_pops
```

Standard import lines:

```python
import pandas as pd
path =  "/Users/harryramsay/Documents/GitHub/Udemy/python-data-science-2022/DataAnalysis"
netflix = pd.read_csv(path + "/data/netflix_titles.csv", sep="|", index_col=0)
netflix
```

# Section 5: Basic Dataframe computations

<details>
<summary>What do you get if you run <code style="white-space:nowrap;">houses.min()</code> over an entire dataframe?
</summary>
Minimum values for every column.
</details>

## `.sum()` & `.count()`

### Using `.count()`

`df.count()` just tells you the non-null values for each column.

### Common `sum()` arguments

Here are some arguments that `.sum()` can take:

```python
df.sum(axis=None, skipna=None, level=None, numeric_only=None, min_count=0, **kwargs)
```

`numeric_only` can be set to `True`, meaning it will only bother with numeric columns.

## Mean, median, mode

- **mean**: average
- **median**: value that is in the middle
- **mode** = the most frequent value

## `.describe()`

Used on its own, `.describe()` will return an analysis of _only_ the numeric columns in the dataframe, with analysis of the following:

- count
- mean
- std
- min
- 25%
- 50%
- 75%
- max

If you add the argument `include=[]`, where you provide a list of datatypes that you want included, it could also work on non-numeric fields too.

```python
titanic.describe(include=['object'])
# or you can simply use a capital O, NOT a lowercase one!
titanic.describe(include=['O'])
```

# Section 6: Series & Columns

## Important series methods

- `head()`
- `tail()`
- `describe()`
- `info()`
- `unique()`
  - Series method **only**. Does not work on dataframes.
- `nunique()`
  - If you’re looking up a series with missing values (i.e. `NaN` or null values), you can optionally add `dropna=False` as a parameter to include the null values in the list of unique values. (By default, null values are skipped.)
- `nlargest()`
  - These are both dataframe and series methods - good for quick analysis.
- `nsmallest()`
  - These are both dataframe and series methods - good for quick analysis.
- `value_counts()`
- `plot()`

> Note on `nlargest()` and `nsmallest()`:
> If there are duplicated values, you can use the `keep=` parameter to pick what you want.

- `first` : prioritize the first occurrence(s)
- `last` : prioritize the last occurrence(s)
- `all` : do not drop any duplicates, even it means selecting more than n items.

```python
# all duplicated values are kept:
df.nlargest(3, 'population', keep='all')
```

## Ranking by one column

```python
houses.nlargest(10,["price"])
```

## Selecting multiple columns

Put a _list_ of items within square brackets.

```python
netflix[["title", "rating"]]
```

## Fundamentals of `value_counts()`

> Returns a Series containing counts of unique values.

(By default, it sorts **descending**. Change with `ascending=True`.)

```python
netflix["director"].value_counts().head(10)
```

You can select a subset of columns and run `value_counts()` on that instead:

```python
houses[["bedrooms", "bathrooms"]].value_counts()
```

## Combining `.plot()` with `.value_counts()` to create a quick plot

> By default, it plots the values against the labels (i.e. the index). This is not always helpful.

```python
houses["bedrooms"].value_counts().plot(kind="bar")
```

```python
netflix["rating"].value_counts().head(10).plot(kind="bar")
```

If you’re using a dataframe (NOT a series), you have the option to assign columns to the X or Y axis. Maybe you want to plot bedrooms against bathrooms?

```python
df = houses[["bedrooms", "bathrooms"]]
df.plot(x="bedrooms", y="bathrooms", kind="scatter")
```

# Section 7: Indexing & Sorting

## Changing the index of a dataframe after importing

```python
btc.set_index("Date", inplace=True)
# Now we can check:
btc.index
```

## Changing the index of a dataframe when importing

If you want to use the first column as the index, set the `index_col` property to 0 when importing.

```python
countries = pd.read_csv(path + "/data/world-happiness-report-2021.csv", index_col=0)
```

## Sorting by values

### Sorting by one column

Use `sort_values()` - this is both a dataframe method and a series method.

```python
countries.sort_values(by="Healthy life expectancy", ascending=False)
```

### Sorting by multiple columns

Simply use a list of columns.

```python
houses.sort_values(["bedrooms", "bathrooms"], ascending=False)
```

**IMPORTANT NOTE!**

> When sorting text, uppercase comes before lowercase. That’s why you might see “de la Cruz” after “Zimmerman”.
>
> To fix this, we can use a key and a lambda to modify (this is weirdly complex and I don’t understand why there isn’t a simple fix like `is_capitalized`...)

Here is the fix:

```python
titanic.sort_values("name", key=lambda col: col.str.lower())
```

## Sorting by index

```python
countries.sort_index()
```

(Does not sort in place by default.)

## Combining sorting and plotting

```python
titanic["pclass"].value_counts().sort_index().plot(kind="bar")
```

or:

```python
houses["bedrooms"].value_counts().sort_index().plot(kind="bar")
```

## Returning data by rows

### `.loc` - by row label

For this, we can use `.loc`.

```python
countries.loc["Yemen"]
```

This finds the row where "Yemen" is the index, and returns the data, albeit _not_ as a dataframe. To get it as a dataframe, wrap it in a second set of square brackets:

```python
countries.loc[["Yemen"]]
```

You can pass multiple arguments as a list:

```python
countries.loc[["Canada", "Mexico", "United States"]]
```

And you can also use slices to select a subset of the data:

```python
titanic.loc[5:10]
```

### `.iloc` - by row position (_integer_ label)

```python
houses.iloc[0:5]
```

### loc & iloc with specific columns

Simply add, as a second argument, the **list** of columns you want.

```python
houses.loc[21612:21611, ["price", "bedrooms"]]
```

**NOTE ON PERFORMANCE**

```python
# 1 - columns specified as argument
countries.loc["Canada": "Denmark", ["Ladder score"]]

#2 - columns specified as an extract
countries.loc["Canada": "Denmark"]["Ladder score"]
```

> In this, the first example is more performant because pandas is able to narrow it down first, before needing to run it on the entire dataset.

# Section 8: Filtering Dataframes

## Filtering dataframes with a boolean series

```python
df["sex"] == "female"
```

This will return a **boolean series** (a column of `True` / `False`). You can take that command and plug it into the entire dataframe by plugging the entire query between a `df[]` command, and this will return a **dataframe**.

```python
df[df["sex"] == "female"]
```

## Filtering with comparison operators

```python
houses[houses["price"] > 500000]
```

## The `between` method

If we want to find houses with between 5 to 7 bathrooms, we can run this to return a boolean series:

```python
houses["bedrooms"].between(5, 7)
```

We then plug it into the `houses` df:

```python
houses[houses["bedrooms"].between(5, 7)
]
```

Finally, we can select only the "bedrooms" column and get a count of the houses which have between 5 and 7 bedrooms:

```python
houses[houses["bedrooms"].between(5, 7)]["bedrooms"].value_counts()
```

## The `isin()` method

Again, boolean series:

```python
netflix_countries = ["Japan", "South Korea", "India"]
netflix["country"].isin(netflix_countries)
```

And now plugging into the dataframe:

```python
netflix[netflix["country"].isin(netflix_countries)]["country"].value_counts()
```

## Combining conditions using AND (&)

```python
women = titanic["sex"] == "female"
died = titanic["survived"] == 0
titanic[women & died]
```

Find the houses which are waterfront but also cost less than $500,000.

```python
is_waterfront = houses["waterfront"] == 1
is_cheap = houses["price"] < 500000
houses[is_waterfront & is_cheap]
```

or, running it differently:

```python
houses[(houses["waterfront"] == 1) & (houses["price"] < 500000)]
```

## Combining conditions using OR (|)

Parentheses matter.

```python
fincher = netflix["director"] == "David Fincher"
scorsese = netflix["director"] == "Martin Scorsese"
recent = netflix["release_year"] > 2015
netflix[(fincher | scorsese) & recent]
```

## Bitwise negation

This is done with the tilde character `~` and essentially means "everything _apart from_ this".

```python
df = titanic.head()
women = df["sex"] == "female"
~women
```

**IMPORTANT NOTE!**

When plugging bitwise negations into a dataframe, you'll need to surround it with parentheses otherwise it won't work properly.

```python
titanic[titanic["survived"] == 0]
# now negate this:
titanic[~(titanic["survived"] == 0)]
```

## Filtering by missing values: `isna` and `notna` methods

Filter by movies that do not have either a director or a cast listed.

```python
netflix[netflix["director"].isna() & netflix["cast"].isna()]
```

# Section 9: Adding & Removing columns

## Dropping values

> (Note: `axis=0` = rows, `axis=1` = columns. Axis is 0 by default.)

```python
# 1 - Using both 'labels' and 'axis'
btc.drop(labels=["SNo", "Name", "Symbol"], axis=1)
# 2 - Using only 'columns'
btc.drop(columns=["SNo", "Name", "Symbol"])
```

How to delete the first three rows?

First get the three rows using the `index` method:

```python
countries.index[0:3]
```

then slot this into the `drop` argument:

```python
countries.drop(countries.index[0:3])
```

Another example: This takes everything from 10 onwards as your selection, and that selection is then dropped (in other words, everything before that will stay in the existing dataframe.)

```python
countries.drop(countries.index[10:])
```

## Adding static columns

Assign a value to a new column name. This appends a new column to the end of the existing dataframe.

```python
titanic["species"] = "human"
```

If you want to insert it in a different position, you can use the `insert` method and specify a column index:

```python
houses.insert(0, "county", "King County")
```

(This creates a new column called "county" in position 0 of the table and populates every value with "King County")

## Adding dynamic columns

### Summing columns

```python
titanic["sibsp"] + titanic["parch"]
```

### Calculating new values for columns

Let's calculate the price by square foot, and then sort by most expensive

```python
houses["price_sqft"] = houses["price"] / houses["sqft_living"]
# now find the most expensive per square foot
houses.sort_values("price_sqft", ascending=False)
```

Do certain zip codes have a higher price per square foot?

```python
houses.sort_values("price_sqft", ascending=False).head(50)["zipcode"].value_counts()
```

# Section 11: Working with Types and NA values

## Casting types with `astype()`

If we want to convert, we can use `astype()`.

- object
- int
- float
- category

This does not work in place.

```python
titanic["age"] = titanic["age"].astype("float")
```

## Introducing the Category type

> **Category** = represents text data where there is a finite number of possible values. Gender is a good example.

Why would you use category as a data type?

> Object allows for any type of value - and sets space accordingly, meaning that it might be taking up much more space than we actually need. Casting to a category type, therefore, might be much more efficient.

```python
titanic["sex"] = titanic["sex"].astype("category")
```

## Casting with pd.to_numeric()

`pd.to_numeric()` can convert columns to numeric values, BUT it also has the benefit of being able to set an error parameter.

- If set to `raise`, it raises an exception.
- if set to `coerce`, it turns any weird, non-castable item (such as question marks) into a NaN value.
- if set to `ignore`, it returns input.

```python
titanic["age"] = pd.to_numeric(titanic["age"], errors="coerce")
```

## dropna() and isna()

`isna()` returns a boolean dataframe demonstrating whether `na` is present. To filter, plug it back into the main dataframe. Let’s look for all rows that don’t have a league, for example:

```python
stats[stats["league"].isna()]
```

### Dropping na values on a series

This returns a new series (original, not modified) with all null values dropped. You can modify the original with inplace=True.

```python
stats["assist"].dropna()
```

### Dropping na values on a dataframe

This works a bit differently to a series `dropna`. By default, it works on **rows** (`axis=0`) but can be set to work on columns with `axis=1`.

- `how=any`
  - Drop the row or column if **any** NaN values are present.
- `how=all`
  - Drop the row or column **only if all values are NaN.**

By default, it uses “any”.

We can also use `subset` to provide a **_list_** of labels that we want it to look at. For example, if we want to drop rows where we don’t have any value for “league”. You could pass multiple columns, if you like.

```python
stats.dropna(subset=["league"])
```

## `fillna` - Replacing na values with another value

This replaces every null value in a dataframe with 0.

```python
stats.fillna(0)
```

If you only want to do this on certain columns, you can provide a dictionary of values to replace with for that column:

```python
stats.fillna({"points": 0, "assists": 0, "rebounds": 0, "league": "amateur"})
```

You can fill with values from another column. Let’s say we want to fill any NaN values in shipping with the existing values in billing.

```python
sales["shipping_zip"].fillna(sales["billing_zip"], inplace=True)
```

# Section 12: Working with Dates & Times

## Converting with pd.to_datetime()

This converts many different items to a datetime object.

```python
pd.to_datetime("2019-12-31")
```

It's extremely flexible with date input formats. All of the following formats are supported, plus more.

```
2019-12-31
2019-31-12
12-31-2019
31-12-2019
31/12/2019
31.12.2019
12-31-19
December 31st 2019
Dec. 31st 19
2019-31-12 11:59pm
2019-31-12 23:59
2019-31-12 23:59:45
```

## Specifying date formats

What if the date is ambiguous, like `10-11-12` ?
You can add `dayfirst=True`. (`yearfirst = True` is also an option.)

We can also specify the specific format we need.

```python
pd.to_datetime("10/11/12", format="%y/%m/%d")
```

[Full documentation for various datetime formats can be found at this link.](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior)

You can be flexible with this, even including text:

```python
pd.to_datetime(meetings, format="%b %d % Y Meeting")
```

This will convert to something like "Dec 11 2019 Meeting", "Jan 6 2019 Meeting", etc.

## Converting columns to datetimes

Does not work in place.

```python
ufos["date_time"] = pd.to_datetime(ufos["date_time"])
```

(Alternatively, use the `parse_dates` argument in `pd.read_csv()` and allow it to be read in correctly from the beginning (it requires a list).)

## Useful `dt` properties

Timeseries and date functionality can be found [here](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#time-date-components).

The following code will return only the "year" component from the "date_time" column.

```python
ufos["date_time"].dt.year
```

You can return the date like this::

```python
ufos["date_time"].dt.date
```

We could count and plot the number of years in which there were sightings:

```python
ufos["date_time"].dt.year.value_counts().head(10).plot(kind="bar")
```

## Comparing Dates

We may want to filter using dates - a date or a time that came before or after `x`. This gives us a boolean series. (Note that you need to use quotes.)

```python
ufos["date_time"] < "1980"
```

You can then "plug this in" to the main dataframe to filter it.

```python
ufos[ufos["date_time"] < "1980"]

```

```python
recent_sightings = ufos[ufos["date_time"].dt.year >= 2018]
recent_sightings.sort_values("date_time")
recent_sightings["date_time"].dt.date.value_counts()
```

## Date math & Timedeltas

The following code returns a "time delta", i.e. a gap between two points in time.

```python
ufos["posted"] - ufos["date_time"]
```

Here's a typical task that may need solving:

- Work with the homes sold between May 1st 2014 and May 1st 2015.
- Within that year, find the waterfront homes that were sold.
- Which quarter of that year had the most waterfront home sales? The least?
- Create a bar plot showing the number of waterfront home sales per quarter.

```python
house_subset = houses[houses["date"].between("2014-05-01", "2015-05-01")]
house_subset[house_subset["waterfront"] == 1]["date"].dt.quarter.value_counts().sort_index().plot(kind="bar")
```

# Section 13: Matplotlib

First import matplotlib.

```python
import matplotlib.pyplot as plt
```

`plt.plot()` takes two arguments - `x` and `y`., as well as other stuff if needed.

x and y need to be “array-like data” (a list, a NumPy array, a pandas Series, etc.)

- If we pass in **two** values, it acts as though it’s `x` then `y`, in that order.
- If we pass in only a **single** value, it treats it as the `y` value. It makes up its own `x` axis, starting at 0 and incrementing by 1.

Note:

- If we use `plt.plot()` in a normal Python file, it **won’t** display.
- If we use it in a Jupyter notebook, it **will** display.
