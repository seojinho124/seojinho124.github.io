---
layout: post
title:  "Pandas Basic Methods"
---
```python
import pandas as pd
hat = pd.read_csv('ch4-1.csv')

# Importing package "pandas" and calling it as pd
# Reading csv file called "ch4-1.csv" using pandas.
# If the data set is in xls or xlsx file, run read_excel()
```


```python
hat
# Checking if the data has been successfully updated
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hatchery</th>
      <th>chick</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>26</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>28</td>
    </tr>
    <tr>
      <th>6</th>
      <td>G</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>




```python
hat.head()
# Give first () values of the data
# When () is not defined, it automatically give 5 values
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hatchery</th>
      <th>chick</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>26</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>24</td>
    </tr>
  </tbody>
</table>
</div>




```python
hat.tail(3)
# Give last (3) values of the data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hatchery</th>
      <th>chick</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>28</td>
    </tr>
    <tr>
      <th>6</th>
      <td>G</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>




```python
hat['chick'].sum()
# Calculatin the sum of all chick int value
```




    194




```python
hat['chick'].mean()
# Calculating mean of chick int value
```




    27.714285714285715




```python
hat['chick'].std()
# Calculating standard deviation of chick int value
```




    2.2146697055682827




```python
hat['chick'].median()
# Calculating median of chick int value
```




    28.0




```python
hat['chick'].min()
# Calculating minimum value in the chick data set
```




    24




```python
hat['chick'].max()
# Calculating maximum value in the chick data set
```




    30




```python
hat. sort_values (by= ['chick'],ascending=True)
# Arranging the data set as min to max.
# If ascending = False, the data set will arrange in max to min.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hatchery</th>
      <th>chick</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>E</td>
      <td>24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>D</td>
      <td>26</td>
    </tr>
    <tr>
      <th>6</th>
      <td>G</td>
      <td>27</td>
    </tr>
    <tr>
      <th>5</th>
      <td>F</td>
      <td>28</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C</td>
      <td>29</td>
    </tr>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>B</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
data = {'Pandas Method': ['Value'],
        'Sum': [194], 'Mean':[27.71], 'STDEV':[2.21], 'Median':[28], 'Minimum':[28], 'Maximum':[30]
        }

df = pd.DataFrame(data)

print(df)

# The table to summarize the methods done above.
```

      Pandas Method  Sum   Mean  STDEV  Median  Minimum  Maximum
    0         Value  194  27.71   2.21      28       28       30



```python

```
