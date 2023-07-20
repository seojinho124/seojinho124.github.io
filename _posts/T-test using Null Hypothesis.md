```python
import pandas as pd
# Importing pandas package
import matplotlib.pyplot as plt
test= pd.read_csv('ch4-3.csv')
# Reading csv file 'ch4-3.csv'
test
# Show test
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
      <th>chick_nm</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>a01</td>
      <td>112</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>a05</td>
      <td>116</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A</td>
      <td>a09</td>
      <td>106</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A</td>
      <td>a12</td>
      <td>104</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A</td>
      <td>a15</td>
      <td>116</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A</td>
      <td>a17</td>
      <td>118</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A</td>
      <td>a26</td>
      <td>110</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A</td>
      <td>a28</td>
      <td>112</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A</td>
      <td>a29</td>
      <td>106</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A</td>
      <td>a30</td>
      <td>108</td>
    </tr>
    <tr>
      <th>10</th>
      <td>B</td>
      <td>b01</td>
      <td>100</td>
    </tr>
    <tr>
      <th>11</th>
      <td>B</td>
      <td>b02</td>
      <td>110</td>
    </tr>
    <tr>
      <th>12</th>
      <td>B</td>
      <td>b07</td>
      <td>98</td>
    </tr>
    <tr>
      <th>13</th>
      <td>B</td>
      <td>b11</td>
      <td>100</td>
    </tr>
    <tr>
      <th>14</th>
      <td>B</td>
      <td>b13</td>
      <td>104</td>
    </tr>
    <tr>
      <th>15</th>
      <td>B</td>
      <td>b17</td>
      <td>112</td>
    </tr>
    <tr>
      <th>16</th>
      <td>B</td>
      <td>b22</td>
      <td>106</td>
    </tr>
    <tr>
      <th>17</th>
      <td>B</td>
      <td>b27</td>
      <td>106</td>
    </tr>
    <tr>
      <th>18</th>
      <td>B</td>
      <td>b28</td>
      <td>96</td>
    </tr>
    <tr>
      <th>19</th>
      <td>B</td>
      <td>b30</td>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>




```python
# As you can see above, A hatchery clearly has more weight.
# Lets test using the box plot.

import seaborn as sns
# Import seabron, a color package.
plt.figure(figsize=(10,7))
# Assign figure size (10w,7h)
sns.boxplot(x='weight', y= 'hatchery' , data = test)
# Box plot using weight as x and hatchery as y.
plt.title('Hatchery A vs B weight distribution', fontsize=17)
# Assign title 'Hatchery A vs B weight distribution'
plt.show()
```


    
![png](output_1_0.png)
    



```python
# By the graph, we know that the A is more heavier.
# But how can we statistically tell whether they have the same value or not?
# We could apply t-test.
# T-test is statistical method that compares the means of two group.
# In order to do t-test, we must check if the two data is normally distributed.
# We use Shapiro-Wilk Test to check the data
import scipy as sp
test_a=test.loc[test.hatchery=='A','weight']
test_b=test.loc[test.hatchery=='B','weight']
```


```python
sp.stats.shapiro(test_a)
```




    ShapiroResult(statistic=0.9400018453598022, pvalue=0.5530338883399963)




```python
sp.stats.shapiro(test_b)
```




    ShapiroResult(statistic=0.9390683770179749, pvalue=0.5426943302154541)




```python
# If the pvalue is higher than 0.05, we say the data is normally distributed.
# If the pvalue is lower than 0.05, we say the data is not normally distributed.
# Since we know that both data are normally distributed, lets excute t-test.
```


```python
sp.stats.ttest_ind(test_a,test_b)
```




    Ttest_indResult(statistic=2.842528280230058, pvalue=0.010803990633924202)




```python
# If the pvalue is lower than 0.05, we say it is within the 95% confidence interval.
# Therefore, we can conclude the dats showing above is correct and both has different weight mean.
# If we let the confidence interval within 99%, we could conclude the mean weight are same. 
```
