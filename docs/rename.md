rename
======

## Renaming a count record in a dataframe.

I had a `groupby` function where I used `.size()` to count the number of records in each row. But the result leaves that dataframe column name as "0".

This is the group:

``` python
people = stops.groupby([
        'HA_N_LAST_DRVR',
        'HA_N_FIRST_DRVR',
        'HA_N_MIDDLE_DRVR']).size().reset_index()
```

And this is the result:

![Data groups](images/rename-groupby.png)

And then it's possible to rename the "size" column, as it is the 3rd one. (Remember counting starts at 0.)

``` python
people.rename(columns={people.columns[2]: "Records" })
```

![Renamed](images/rename-done.png)

## Rename multiple columns

Create a dictionary with the old name and then new name for each column. Then pass that into the `.rename()` function.

```python
our_columns = {
    "tradename" : "TradeName",
    "ll_streetaddressnbr" : "Numb",
    "ll_addressline1" : "Street",
    "ll_cityname" : "City",
    "ll_countyname" : "County",
    "allSub" : "Licences"
}
df_renamed = df.rename(index=str, columns=our_columns)
```

