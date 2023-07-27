---
layout: post
title:  "Regression Analysis"
---

```python
# Regression Analysis is simply a way to find the correlation in linear format.
# In order to do regression analysis, 5 conditions must meet.
# 1. Linear: is independant valuable (x) linearly related to dependent valuable (y).
# 2. Dependent: Dependant valuable must be dependent from residual.
# 3. All error distribution of independant valuable must be normal. 
# 4. Non-inertial: All observed residual must be non-inertial.
# 5. Normality: All residual must be normally distributed.
```


```python
import pandas as pd
w=pd.read_csv('ch5-1.csv')
w_n=w.iloc[:,1:5]
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.formula.api as smf
model_lm=smf.ols(formula='weight ~ egg_weight',data=w_n)
result_lm=model_lm.fit()
print(result_lm.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       0.916
    Model:                            OLS   Adj. R-squared:                  0.913
    Method:                 Least Squares   F-statistic:                     306.0
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):           1.32e-16
    Time:                        15:28:47   Log-Likelihood:                -63.148
    No. Observations:                  30   AIC:                             130.3
    Df Residuals:                      28   BIC:                             133.1
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept    -14.5475      8.705     -1.671      0.106     -32.380       3.285
    egg_weight     2.3371      0.134     17.493      0.000       2.063       2.611
    ==============================================================================
    Omnibus:                       15.078   Durbin-Watson:                   1.998
    Prob(Omnibus):                  0.001   Jarque-Bera (JB):                2.750
    Skew:                           0.032   Prob(JB):                        0.253
    Kurtosis:                       1.518   Cond. No.                     1.51e+03
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 1.51e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.



```python
# Prob(F-statistics) is telling whether the data is reliable. The value should be lower than 0.05.
# P>|t| is showing the p-value for each dependant valuable
# coef is telling the coefficient for the valuable
```


```python
# Since we know the values required to plot the linear equation.
# Lets start plotting.
plt.figure(figsize=(10,6))
plt.scatter(w.egg_weight,w.weight,alpha = .5)
plt.plot(w.egg_weight, w.egg_weight*2.3371-14.5475)
# Recall the format plot(x,y).
plt.text(66,132,'weight=2.3371egg_weight-14.5475', fontsize=12)
# text(66,132) is assigning where I want the "weight=2.3371egg_weight-14.5475" displayed.
plt.title("Scatter Plot")
plt.xlabel('egg_weight')
plt.ylabel('weight')
plt.show()
```


    
![png](output_3_0.png)
    



```python
result_lm.resid.head()
# Showing the residual applied to result_lm
```




    0    2.633714
    1   -2.354880
    2    2.633714
    3   -2.366286
    4   -1.714829
    dtype: float64




```python
plt.figure(figsize=(10,6))
plt.hist(result_lm.resid,bins=7)
plt.show()
# Plotting the residual in histogram.
```


    
![png](output_5_0.png)
    



```python
# The best data would be where residual are distributed near the 0.
# How could we make it better?
# We could try Multiple Regression Analysis
# Multiple Regression Analysis is analysis of multiple dependant valuable
# The regression equation looks something like this y=ax1+bx2+c
```


```python
model_mlm=smf.ols(formula='weight~egg_weight+food+movement',data=w_n)
# When adding a dependant valuable use +. 
result_mlm=model_mlm.fit()
```


```python
print(result_mlm.summary())
print(result_lm.summary())

# As you can see R-squared increased and Prob(F-stat) decreased
# However, P>|t| for movement is higher than 0.05 meaning movement should be removed for the analysis
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       0.948
    Model:                            OLS   Adj. R-squared:                  0.942
    Method:                 Least Squares   F-statistic:                     157.7
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):           8.46e-17
    Time:                        15:41:15   Log-Likelihood:                -56.008
    No. Observations:                  30   AIC:                             120.0
    Df Residuals:                      26   BIC:                             125.6
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept      2.9748      8.587      0.346      0.732     -14.676      20.626
    egg_weight     1.7763      0.195      9.117      0.000       1.376       2.177
    food           1.5847      0.405      3.915      0.001       0.753       2.417
    movement      -0.0087      0.017     -0.522      0.606      -0.043       0.026
    ==============================================================================
    Omnibus:                        1.993   Durbin-Watson:                   2.030
    Prob(Omnibus):                  0.369   Jarque-Bera (JB):                1.746
    Skew:                          -0.480   Prob(JB):                        0.418
    Kurtosis:                       2.311   Cond. No.                     4.31e+03
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 4.31e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.
                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       0.916
    Model:                            OLS   Adj. R-squared:                  0.913
    Method:                 Least Squares   F-statistic:                     306.0
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):           1.32e-16
    Time:                        15:41:15   Log-Likelihood:                -63.148
    No. Observations:                  30   AIC:                             130.3
    Df Residuals:                      28   BIC:                             133.1
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept    -14.5475      8.705     -1.671      0.106     -32.380       3.285
    egg_weight     2.3371      0.134     17.493      0.000       2.063       2.611
    ==============================================================================
    Omnibus:                       15.078   Durbin-Watson:                   1.998
    Prob(Omnibus):                  0.001   Jarque-Bera (JB):                2.750
    Skew:                           0.032   Prob(JB):                        0.253
    Kurtosis:                       1.518   Cond. No.                     1.51e+03
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 1.51e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.



```python
# So lets try another multiple regression analysis excluding movement
model_mlm2=smf.ols(formula='weight~egg_weight+food',data=w_n)
result_mlm2=model_mlm2.fit()
print(result_mlm2.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       0.947
    Model:                            OLS   Adj. R-squared:                  0.943
    Method:                 Least Squares   F-statistic:                     243.0
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):           5.44e-18
    Time:                        15:45:59   Log-Likelihood:                -56.164
    No. Observations:                  30   AIC:                             118.3
    Df Residuals:                      27   BIC:                             122.5
    Df Model:                           2                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept      3.6638      8.370      0.438      0.665     -13.510      20.837
    egg_weight     1.7453      0.183      9.536      0.000       1.370       2.121
    food           1.5955      0.399      4.001      0.000       0.777       2.414
    ==============================================================================
    Omnibus:                        2.302   Durbin-Watson:                   2.103
    Prob(Omnibus):                  0.316   Jarque-Bera (JB):                1.940
    Skew:                          -0.502   Prob(JB):                        0.379
    Kurtosis:                       2.263   Cond. No.                     1.84e+03
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 1.84e+03. This might indicate that there are
    strong multicollinearity or other numerical problems.



```python
# Remember, multiple regression may not give accurate regression since there are too many valuable.
# We call this a multicollinearity probelm.
# In order to find if there are multicollinearity problem, we check for Variance Inflation Factor (VIF).
```


```python
import statsmodels.formula.api as smf
from statsmodels.stats.outliers_influence import variance_inflation_factor
model_mlm2.exog_names
```




    ['Intercept', 'egg_weight', 'food']




```python
vif1=variance_inflation_factor(model_mlm2.exog,1)
vif2=variance_inflation_factor(model_mlm2.exog,2)
print(vif1,vif2)
```

    2.88268451130757 2.8826845113075756



```python
# We say there are no probelm if VIF is lower than 10.
# Since both VIF is lower than 10, we visualize the residiual distribution again

plt.figure(figsize=(10,6))
plt.hist(result_mlm2.resid,bins=7)
plt.show()
```


    
![png](output_13_0.png)
    



```python
# We could see that the distribution is much more closer to 0. 
# Therefore, we could conclude the regression to be weight=1.7453*egg_weight+1.5955*food+3.6638
```


```python
# Now lets try Non-Regression Analysis where x and y is not linearly proportional.
w2=pd.read_csv('ch5-2.csv')
w2.head()
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
      <th>day</th>
      <th>weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>55</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>104</td>
    </tr>
  </tbody>
</table>
</div>




```python
w2.info()
# This is a dataset that shows weight gained per day.
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 70 entries, 0 to 69
    Data columns (total 2 columns):
     #   Column  Non-Null Count  Dtype
    ---  ------  --------------  -----
     0   day     70 non-null     int64
     1   weight  70 non-null     int64
    dtypes: int64(2)
    memory usage: 1.2 KB



```python
plt.figure(figsize=(10,6))
plt.scatter(w2.day, w2.weight)
plt.title('Scatter Plot')
plt.xlabel('day')
plt.ylabel('weight')
plt.show()
```


    
![png](output_17_0.png)
    



```python
# As we see, the data is not appropriate for linear regression analysis
# But lets try how it looks.

model_lm2=smf.ols(formula='weight~day',data=w2)
result_lm2=model_lm2.fit()
print(result_lm2.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       0.979
    Model:                            OLS   Adj. R-squared:                  0.979
    Method:                 Least Squares   F-statistic:                     3189.
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):           7.22e-59
    Time:                        16:18:55   Log-Likelihood:                -457.86
    No. Observations:                  70   AIC:                             919.7
    Df Residuals:                      68   BIC:                             924.2
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept   -295.8671     41.102     -7.198      0.000    -377.885    -213.850
    day           56.8216      1.006     56.470      0.000      54.814      58.830
    ==============================================================================
    Omnibus:                        3.866   Durbin-Watson:                   0.025
    Prob(Omnibus):                  0.145   Jarque-Bera (JB):                2.079
    Skew:                          -0.133   Prob(JB):                        0.354
    Kurtosis:                       2.199   Cond. No.                         82.6
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.



```python
# It does have high R-squared and low Prob(F-stats) and low P>|t| value
# Lets try graphing it
plt. figure(figsize=(10,6))
plt.scatter(w2.day,w2.weight)
plt.plot(w2.day,w2.day*56.8216-295.8671,color='red')
plt.text(40,500,'weight=56.821day-295.8671', fontsize=12)
plt.title('Scatter Plot')
plt.xlabel('day')
plt.ylabel('weight')
plt.show()
```


    
![png](output_19_0.png)
    



```python
# As we can see, it is somewhat not so fitted to the data.
# Therefore, lets try making a quadratic function
```


```python
model_nlm=smf.ols(formula='weight~I(day**3)+I(day**2)+day',data=w2)
result_nlm=model_nlm.fit()
print(result_nlm.summary())
```

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                 weight   R-squared:                       1.000
    Model:                            OLS   Adj. R-squared:                  0.999
    Method:                 Least Squares   F-statistic:                 4.407e+04
    Date:                Thu, 27 Jul 2023   Prob (F-statistic):          7.13e-109
    Time:                        16:27:56   Log-Likelihood:                -327.17
    No. Observations:                  70   AIC:                             662.3
    Df Residuals:                      66   BIC:                             671.3
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ===============================================================================
                      coef    std err          t      P>|t|      [0.025      0.975]
    -------------------------------------------------------------------------------
    Intercept     117.0141     13.476      8.683      0.000      90.108     143.920
    I(day ** 3)    -0.0253      0.000    -51.312      0.000      -0.026      -0.024
    I(day ** 2)     2.6241      0.053     49.314      0.000       2.518       2.730
    day           -15.2978      1.632     -9.373      0.000     -18.557     -12.039
    ==============================================================================
    Omnibus:                        6.702   Durbin-Watson:                   0.082
    Prob(Omnibus):                  0.035   Jarque-Bera (JB):                2.680
    Skew:                           0.103   Prob(JB):                        0.262
    Kurtosis:                       2.064   Cond. No.                     5.65e+05
    ==============================================================================
    
    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 5.65e+05. This might indicate that there are
    strong multicollinearity or other numerical problems.



```python
# As we can see, R-squared is now 1 and Prob(F-stat) much lower
# Now lets graph it and see
```


```python
plt.figure(figsize=(10,6))
plt.scatter(w2.day,w2.weight)
plt.plot(w2.day,(w2.day**3)*(-0.0253)+(w2.day**2)*2.6241+w2.day*(-15.2978)+117.0141,color='red')
plt.text(0,3200,'weight=-0.02532(day^3)+2.6241(day^2)-15.2978day+117.0141',fontsize=12)
plt.title('Scatter Plot')
plt.xlabel('day')
plt.ylabel('weight')
plt.show()
```


    
![png](output_23_0.png)
    



```python
# Since the data and quadratic function are nearly identical
# We can conclude that the Weight=-0.02532(day^3)+2.6241(day^2)-15.2978day+117.0141.
```
