#Imports

## Basic import from csv

## Convert to datetime

Include `parse_dates=True` in your import command to have pandas sniff out date columns. To ensure specific fields are imported s a date, you can pass it a list of columns that are dates:

``` python
df = pd.read_csv(
    '../access-exports/test-converted.csv',
    index_col=None,
    parse_dates=['HA_ARREST_DATE']
    )
```

There are [other options](http://pandas.pydata.org/pandas-docs/version/0.20/generated/pandas.read_csv.html?highlight=parse_dates).

## Setting data types for columns

I had a case where I wanted to set the datatype of all the columns on an import, but I also had dates. There is an option to [set the dtype upon import](https://pandas.pydata.org/pandas-docs/stable/io.html#specifying-column-data-types), but I got an error when trying to use datatime as an option, and also when using `parse_dates=` at the same import.

So, I implicitly set the dates as strings upon import, then re-assigned them as dates afterward:

``` python
column_types = {
    "NAME_COL": pd.np.str,
    "DATE_COL_01": pd.np.str,
    "DATE_COL_02": pd.np.str
}

# import raw data
data_raw = pd.read_csv('path_to_data', index_col=None, dtype=column_types)

dates_fixed = df.assign(
    NEW_DATE_COL_01 = pd.to_datetime(data_raw['DATE_COL_01']),
    NEW_DATE_COL_02 = pd.to_datetime(data_raw['DATE_COL_02']),
)
```

## Encoding errors

If you get an import error about a codec, like `UnicodeDecodeError: 'utf-8' codec can't decode byte 0xd1 in position 2: invalid continuation byte`, then you can set encoding on import:

``` python
data_raw = pd.read_csv(
    'path_to_data',
    index_col=None,
    encoding="ISO-8859-1"
    )
```

## Dealing with Mr. Null

I had a case where I wanted to keep a cell value as "NULL". This can be done with a combination of [`keep_default_na` and `na_values`](http://pandas.pydata.org/pandas-docs/version/0.13.1/io.html#na-values)

``` python
data_raw = pd.read_csv(
    'path_to_data',
    index_col=None,
    keep_default_na=False,
    na_values=[""]
    )
```

The `na_values` list could be a list of more values, as noted [in docs](http://pandas.pydata.org/pandas-docs/version/0.13.1/io.html#na-values).

## fillna all the time?

Right now, I'm thiking it is good practice to fill `NaN` fields with blank text, because if you use `groupby`, it excludes any records that have `NaN` as a "value" in the grouping key. So, if you are grouping on `first_name`, `last_name` and `middle_name`, records with no `middle_name` would be excluded. Use `fillna` to make that a blank cell, and it is then included in the `groupby`.

The answer, I think, is to use `fillna` [after importing](http://pandas.pydata.org/pandas-docs/version/0.13.1/generated/pandas.DataFrame.fillna.html) data into a dataframe:

``` python
data_filled = data_raw.fillna('')
```

## Combine multiple sheets and tabs

Ben Welsh [walks through this](https://github.com/palewire/pandas-combine-workbooks-example/blob/master/pandas-combine-workbooks-example.ipynb).