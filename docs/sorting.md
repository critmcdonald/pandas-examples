Sorting dataframes
===================

## Sort by a single column

``` python
df.sort_values('NUM_CASES'], ascending=False)
```

Above assumes ascending is true, so make false to reverse sort.

## Sorting multiple columns

``` python
df.sort_values(by=['NUM_CASES', 'LAST_NAME'], ascending=[0, 1])
```

The above would sort first by NUM_CASES descending, then LAST_NAME ascending.
