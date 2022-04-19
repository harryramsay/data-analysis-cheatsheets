# Common Excel functions in pandas

Given that Excel is so widely used for data analysis, it makes sense to be able to replicate its most widely-used functions in pandas just as fluently. This document will break down ways to do this.

# Sorting Data

In Excel, you need to be able to sort by a given column. This is done in pandas with the `sort_values()` method.

Here it is applied to the `sales` dataframe, sorted by revenue. (Note that it is sorted in descending order.) We are also using `head()` to limit it to the top 5 results.

You can use either a string or a list of strings for the column name to sort by.

```python
sales.sort_values(["Revenue"], ascending=False).head(5)
```
