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
