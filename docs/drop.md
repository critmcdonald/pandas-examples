# Drop a column from a dataframe

Remove one or more columns from a dataframe by assigning it back using the [.drop](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.drop.html) method.

The `1` means to drop columns instead of rows.

``` python
df = df.drop('COLUMN NAME', 1)
```

- Can drop multiple columns by putting them in a list: `.drop(['COL NAME 01', 'COL NAME 02'])`.
- Can drop by the index of the column by using position number: `.drop(0, 1)` would drop the first column.