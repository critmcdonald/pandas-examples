Melt
====

Thought to pursue this, since I've had to do it in agate:

https://stackoverflow.com/questions/32105368/pandas-dataframe-reshaping-stacking-of-multiple-value-variables-into-seperate-co

I like this answer:

``` python
d = {'des1' : ['', 'a', 'd', 'g'],
     'des2' : ['', 'b', 'e', 'h'],
     'des3' : ['', 'c', 'f', 'i'],
     'interval1' : ['', '##1', '##4', '##7'],
     'interval2' : ['', '##2', '##5', '##6'],
     'interval3' : ['', '##3', '##6', '##9']}

df = pd.DataFrame(d, index=['value', 'aaa', 'bbb', 'ccc'], 
                  columns=['des1', 'des2', 'des3', 'interval1', 'interval2', 'interval3'])

nd = {'des' : [''] + df.iloc[1, 0:3].tolist() + df.iloc[2, 0:3].tolist() + df.iloc[3, 0:3].tolist(),
      'interval' : ['']+ df.iloc[1, 3:6].tolist() + df.iloc[2, 3:6].tolist() + df.iloc[3, 3:6].tolist()}

ndf = pd.DataFrame(nd, index=['value', 'aaa', 'aaa', 'aaa', 'bbb', 'bbb', 'bbb', 'ccc', 'ccc', 'ccc'], columns=['des', 'interval'])
```