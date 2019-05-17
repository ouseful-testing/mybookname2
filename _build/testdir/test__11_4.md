---
redirect_from:
  - "/testdir/test--11-4"
title: 'test__11_4'
prev_page:
  url: /testdir/test__11_3
  title: 'test__11_3.md'
next_page:
  url: /testdir/test__11_5
  title: 'test__11_5'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---
# 2 Every picture tells a story


It can be difficult and confusing to look at a table of rows of numbers and make any meaningful interpretation especially if there are many rows and columns.

Handily, pandas has a method called `__plot()__` which will visualise data for us by producing a chart.

Before using the `__plot()__` method, the following line of code must be executed (once) which tells Jupyter to display all charts inside this notebook, immediately after each call to `__plot():__`

`__In []:__`

`%matplotlib inline`

To plot `__‘Max Wind SpeedKm/h__` ’, it’s as simple as this code:

`__In []:__`

`london['Max Wind SpeedKm/h'].plot(grid=True)`

`__Out[]:__`


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1023.jpg)
__Figure 10__

Chart of the values in the Max Wind SpeedKm/h column of the london dataframe. 
The `__grid=True__` argument makes the gridlines (the dotted lines in the image above) appear, which make values easier to read on the chart. The chart comes out a bit small, so you can make it bigger by giving the `__plot()__` method some extra information. The figsize units are inches.

`__In []:__`

`
london['Max Wind SpeedKm/h'].plot(grid=True, figsize=(10,5))
`

`__Out[]:__`


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1024.jpg)
__Figure 11__

Larger version of the first chart on this page
That’s better! The argument given to the `__plot()__` method, `__figsize=(10,5)__` simply tells `__plot()__` that the x-axis should be 10 units wide and the y-axis should be 5 units high. In the above graph the x-axis (the numbers at the bottom) shows the dataframe’s index, so 0 is 1 January and 50 is 18 February.

The y-axis (the numbers on the side) shows the range of wind speed in kilometres per hour. It is clear that the windiest day in 2014 was somewhere in mid-February and the wind reached about 66 kilometers per hour.

By default, the `__plot()__` method will try to generate a line, although as you’ll see in a later week, it can produce other chart types too.


### Exercise 5 Every picture tells a story


#### Question

Now try Exercise 5 in the Exercise notebook 2.

If you’re using Anaconda, remember that to open the notebook you’ll need to navigate to the notebook using Jupyter.




## 2.1 Changing a dataframe’s index


We have seen that by default every dataframe has an integer index for its rows which starts from 0.

The dataframe we’ve been using, `__london__` , has an index that goes from `__0__` to `__364__`. The row indexed by `__0__` holds data for the first day of the year and the row indexed by `__364__` holds data for the last day of the year. However, the column `__'GMT'__` holds `__datetime64__` values which would make a more intuitive index.

Changing the index to `__datetime64__` values is as easy as assigning to the dataframe’s `__index__` attribute the contents of the `__'GMT'__` column, like this:

`__In []:__`


```python

london.index = london['GMT']
#Display the first 2 rows
london.head(2)
```


`__Out[]:__`


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1011.jpg)
__Figure 12__

First 2 rows of the london dataframe showing that the index has been changed to the datetime64 values from the GMT column. Note that only the first few columns are shown due to the limitation of page width. 
* Note that the right of the table has been cropped to fit on the page. *

Notice that the `__'GMT'__` column still remains and that the index has been labelled to show that it has been derived from the `__'GMT'__` column.

You can still access a row using the `__iloc__` attribute, so to get the first line in the dataframe you can simply execute:

`__In []:__`

`london.iloc[0]`

`__Out[]:__`


```python

GMT 2014-01-01 00:00:00
Max TemperatureC 11
Mean TemperatureC 8
Min TemperatureC 6
Dew PointC 9
MeanDew PointC 7
Min DewpointC 4
Max Humidity 94
Mean Humidity 86
Min Humidity 73
Max Sea Level PressurehPa 1002
Mean Sea Level PressurehPa 993
Min Sea Level PressurehPa 984
Max VisibilityKm 31
Mean VisibilityKm 11
Min VisibilitykM 2
Max Wind SpeedKm/h 40
Mean Wind SpeedKm/h 26
Max Gust SpeedKm/h 66
Precipitationmm 9.91
CloudCover 4
Events Rain
WindDirDegrees 186
Name: 2014-01-01 00:00:00, dtype: object
```


But now you can now also use the `__datetime64__` index to get a row using the dataframe’s `__loc__` attribute, like this:

`__In []:__`

`london.loc[datetime(2014, 1, 1)]`

`__Out[]:__`


```python

GMT 2014-01-01 00:00:00
Max TemperatureC 11
Mean TemperatureC 8
Min TemperatureC 6
Dew PointC 9
MeanDew PointC 7
Min DewpointC 4
Max Humidity 94
Mean Humidity 86
Min Humidity 73
Max Sea Level PressurehPa 1002
Mean Sea Level PressurehPa 993
Min Sea Level PressurehPa 984
Max VisibilityKm 31
Mean VisibilityKm 11
Min VisibilitykM 2
Max Wind SpeedKm/h 40
Mean Wind SpeedKm/h 26
Max Gust SpeedKm/h 66
Precipitationmm 9.91
CloudCover 4
Events Rain
WindDirDegrees 186
Name: 2014-01-01 00:00:00, dtype: object
```


A query such as ‘Return all the rows where the date is between 8 December and 12 December’ which you did before (and can still do) with:

`__In []:__`


```python

london[(london['GMT'] >= datetime(2014, 12, 8))
    & (london['GMT'] <= datetime(2014, 12, 12))]
```


can now be done more succinctly like this:

`__In []:__`


```python


london.loc[datetime(2014,12,8) : datetime(2014,12,12)]



#The meaning of the above code is get the rows between

#and including the indices datetime(2014,12,8) and
#datetime(2014,12,12)
```


`__Out[]:__`


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1012.jpg)
__Figure 13__

Rows from the london dataframe where the index is between 2014-12-08 and 2014-12-12 (inclusive). Note that only the first few columns are shown due to the limitation of page width. 
* Note that the right of the table has been cropped to fit on the page. *

Because the table is in date order, we can be confident that only the rows with dates between 8 December 2014 and 12 December 2014 (inclusive) will be returned. However if the table had not been in date order, we would have needed to sort it first, like this:

`london = london.sort_index()`

Now there is a `__datetime64__` index, let’s plot ' `__Max Wind SpeedKm/h__` 'again:

`__In []:__`

`
london['Max Wind SpeedKm/h'].plot(grid=True, figsize=(10,5))
`

`__Out[]:__`


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1013.jpg)
__Figure 14__

Chart of the values in the Max Wind SpeedKm/h column of the london dataframe. Note that the legend for the x-axis has changed from numbers to month names. 
Now it is much clearer that the worst winds were in mid-February.


### Exercise 6 Changing a dataframe’s index


#### Question

Now try Exercise 6 in the Exercise notebook 2.




## 2.2 The project


Your project this week is to find out what would have been the best two weeks of weather for a 2014 vacation in a capital of a BRICS country.


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1039.jpg)
__Figure 15__

An image of filter like diagonal strips across various skies such as an orange sunset, a storm and a clear blue sky 
I’ve written up my analysis of the best two weeks of weather in London, UK, which you can open in project: 2: Holiday weather.

The structure is very simple: besides the introduction and the conclusions, there is one section for each step of the analysis – obtaining, cleaning and visualising the data.

Once you’ve worked through my analysis you should open a dataset for just one of the BRICS capitals: Brasilia, Moscow, Delhi, Beijing or Cape Town. The choice of capital is up to you. You should then work out the best two weeks, according to the weather, to choose for a two-week holiday in your chosen capital city.

Download the dataset for your chosen location as follows:
* Right click on the name of your chosen capital city aboveRight click on the name of your chosen capital city above
* Choose to save the file via ‘Download Linked File As...’ Save the file with its default name to your downloads folder.Choose to save the file via ‘Download Linked File As...’ Save the file with its default name to your downloads folder.
* If necessary, rename the file so that it has a .csv extension.If necessary, rename the file so that it has a .csv extension.
* Finally, move or copy te file to the disk folder or SageMathCloud by Cocalc project you created in Week 1.Finally, move or copy te file to the disk folder or SageMathCloud by Cocalc project you created in Week 1.

Once again, __do not open the file with Excel__ , but you could take a look using a text editor.

In my project, because I’m in London, which is often cold and rainy, I was looking for a two week period that had relatively high temperatures and little rain. If you choose a capital in a particularly hot and dry country you will probably be looking for relatively cool weather and low humidity.

Note that the London file has the dates in a column named ‘GMT’ whereas in the BRICS files they are in a column named ‘Date’. You will need to change the Python code accordingly. You should also change the name of the variable, London, according to the capital you choose.

