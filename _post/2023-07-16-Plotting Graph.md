defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
    
```python
import pandas as pd
hat = pd.read_csv('ch4-1.csv')
# Importing pandas
# Importing csv file "ch4-1.csv" using pandas package
```


```python
import matplotlib.pyplot as plot
# Importing matplot
```


```python
plot.bar(hat['hatchery'],hat['chick'])
plot.show()
# Plotting bar graph of 'hatchery' vs 'chick'
```


    
![png](output_2_0.png)
    



```python
plot.figure(figsize=(10,7))
# Setting figure size to 10 width and 7 height
plot.bar(hat['hatchery'],hat['chick'],color=('red','orange','yellow','green','blue','navy','purple'))
# Assigning bar color
plot.title('chick born per hatchery')
# Assigning title for the graph
plot.xlabel('hatchery')
# Assigning x-axis label
plot.ylabel('chick')
# Assigning y-axis label
plot.show()
```


    
![png](output_3_0.png)
    



```python
import seaborn as sns
# Importing seaborn package
col7 = sns.color_palette ('Pastel2',7)
# Choosing the color selection(Pastel2)
plot.figure(figsize=(10,7))
# Setting figure size (10w,7h)
plot.bar(hat['hatchery'],hat['chick'],color=col7,edgecolor='black')
# Assigning Color
```




    <BarContainer object of 7 artists>




    
![png](output_4_1.png)
    



```python
def addtext(x,y):
    for i in range(len(x)):
        plot.text(i,y[i]+0.5,y[i],ha='center')
# Defining addtext() function
```


```python
import seaborn as sns
# Importing seaborn package
col7 = sns.color_palette ('Pastel2',7)
# Choosing the color selection(Pastel2)
plot.figure(figsize=(10,7))
# Setting figure size (10w,7h)
plot.bar(hat['hatchery'],hat['chick'],color=col7,edgecolor='black')
# Assigning Color
addtext(hat['hatchery'],hat['chick'])
# Assigning value on top of the bar
plot.title('chick born per hatchery')
# Assigning title for the graph
plot.xlabel('hatchery')
# Assigning x-axis label
plot.ylabel('chick')
# Assigning y-axis label
plot.show()
```


    
![png](output_6_0.png)
    



```python
import seaborn as sns
# Importing seaborn package
col7 = sns.color_palette ('Pastel2',7)
# Choosing the color selection(Pastel2)
plot.figure(figsize=(10,7))
# Setting figure size (10w,7h)
plot.bar(hat['hatchery'],hat['chick'],color=col7,edgecolor='black')
# Assigning Color
addtext(hat['hatchery'],hat['chick'])
# Assigning value on top of the bar
plot.hlines(30,-1,7, colors='red',linestyles='dashed')
# Add dashed red lin on top(30 height, -1 x-start point, 7 x-end point)
plot.title('chick born per hatchery')
# Assigning title for the graph
plot.xlabel('hatchery')
# Assigning x-axis label
plot.ylabel('chick')
# Assigning y-axis label
plot.show()
```


    
![png](output_7_0.png)
    



```python

```


```python
#Now using the same application, Lets create pie chart
pct=hat['chick']/hat['chick'].sum()
pct
#Calculating the ratio inside the dataset
```




    0    0.154639
    1    0.154639
    2    0.149485
    3    0.134021
    4    0.123711
    5    0.144330
    6    0.139175
    Name: chick, dtype: float64




```python
plot.figure(figsize=(10,10))
# Setting the figure size
plot.pie(pct,labels = hat['hatchery'],autopct='%.1f%%',colors=col7,startangle=90,counterclock=False)
# Setting the labels.
# Autopct is to set the parameter. %.1f%% means show until the first decimal point. 
# If %.2f$$, it will show for the second decimal point
# Startangle is to set the starting pie data angle
# Counterclock = False shows the data in clockwise.
plot.show()
```


    
![png](output_10_0.png)
    



```python
# For more practice, explore more parameter setting by pressing "Shift+Tab" for the following line. 
```
