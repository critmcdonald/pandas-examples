Merge/Join/Concat
==========

## Merge by joining in a key
To replicate a SQL-like join, you would use `pd.merge`.

``` python
joined = pd.merge(df_a, df_b, on='key_column', how='inner')
```
- `key_column` is the column that is the same in both data frames.
- `how` is the type of join: left, right, inner, outer.

There are many options, as noted by [Albon](https://chrisalbon.com/python/data_wrangling/pandas_join_merge_dataframe/) and [Pandas docs](https://pandas.pydata.org/pandas-docs/stable/merging.html).

## Merge by stacking two files

To stack one datafram on top of another one, assuming they have the same columns.

``` python
df_new = pd.concat([df_a, df_b])
```
