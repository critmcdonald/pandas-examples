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
