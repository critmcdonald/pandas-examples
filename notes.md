Pandas appears to be a reasonable approach here. Based on what you've described of the Excel function, I'd check out the documentation for the DataFrame.apply method, which allows you to pass through a function and either apply that function to each column or apply it to each row.

So you could create a function like

```
def dothis(x):
if [condition 1]:
return [something]
```

etc

And then create a field within your DataFrame passing each row through that function:

```
df [ 'NewColumn' ] = df.apply(dothis, axis=1)
```


H/T Max Lee, The Northern Virginia Daily

## filter, get value counts, normalize

```python
ri[ri.driver_gender == "F"].violation.value_counts(normalize=True)
```

from [intermediate tutorial](https://github.com/justmarkham/pycon-2018-tutorial)

## str.contains()

when you want to look throug the values of a column for a string and count how many rows has that string. `ri` is my dataframe.

``` python
ri['frisk'] = ri.search_type.str.contains('Protective Frisk')
ri.frisk.value_counts()
```

