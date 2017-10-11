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

I had a case where I wanted to set the datatype of all the columns on an import, but I also had dates. There is an option to [set the dtype upon import](https://pandas.pydata.org/pandas-docs/stable/io.html#specifying-column-data-types, but I got an error when trying to use datatime as an option, and also when using `parse_dates=` at the same import.

So, I implicitly set the dates as strings upon import, then re-assigned them as dates afterward:

``` python
column_types = {
    "NAME_COL": pd.np.str,
    "DATE_COL": pd.np.str
}

# import raw data
data_raw = pd.read_csv('path_to_data', index_col=None, dtype=column_types)

# assign var to fix the dates
fix_date = pd.to_datetime(data_raw['DATE_COL'])
# create new df, assigning value of the coverted string to date
data_fixed = data_raw.assign(DATE_COL_FIXED = fix_date)
```