# Create column based on dividing two columns

This uses the method `.vectorize` method and a function to try if a math operation will work before setting the new column to a value. This is useful if you are getting a `ZeroDivisionError`.

There are probably other ways to do this, but it works.

``` python
# set up the function for the math
def per_student(x, y):
    """Test if zero. Divide to get per student ratio."""

    if y == 0:
        return np.nan
    else:
        return x / y
    
data['ADA_PER_STUDENT'] = np.vectorize(per_student)(data['FUNDING'], data['ADA'])
data['WADA_PER_STUDENT'] = np.vectorize(per_student)(data['FUNDING'], data['WADA'])
```