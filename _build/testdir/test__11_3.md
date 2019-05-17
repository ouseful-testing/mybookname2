---
redirect_from:
  - "/testdir/test--11-3"
interact_link: content/testdir/test__11_3.ipynb
kernel_name: python3
has_widgets: false
title: 'test__11_3.ipynb'
prev_page:
  url: /testdir/test__10_6
  title: 'test__10_6'
next_page:
  url: /testdir/test__11_4
  title: 'test__11_4'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# 1 Loading the weather data

You have learned some more about Python and the pandas module and tried it out on a fairly small dataset. You are now ready to explore a dataset from the Weather Underground.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1039.jpg)
__Figure 1__

An image of filter like diagonal strips across various skies such as an orange sunset, a storm and a clear blue sky 
Open the file London_2014.csv and save it in the disk folder or CoCalc project you created in Week 1.

__Do not be tempted to open this file with Excel__ as this application will attempt to localise the data in the file, i.e. use your country’s local data formats, which will make much of what follows rather incomprehensible! You can if you like open the file with a simple text editor, but __do not make any changes__.

The CSV file can be loaded into a dataframe by executing the following code:

`__In []:__`




{:.input_area}
```python

from pandas import *
london = read_csv('London_2014.csv')
london.head()
```


`__Out[]:__`

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1006.jpg)
__Figure 2__

First 5 rows of the london dataframe. Note that only the first few columns are shown due to the limitation of page width. 
* Note that the right hand side of the table has been cropped to fit on the page. *

In the next section, you’ll find out how to remove rogue spaces.

---

### Important notice for learners outside of the EU

The Weather Underground automatically localises data based on from what country it detects you are accessing the web site. So, for example, if you are accessing the website from the USA wind speeds will be in MPH rather than km/h and temperatures in Fahrenheit rather than Celsius.

In order to change the settings so that the data is in European format you will need to click on the ‘head and shoulders’ icon on the top right of the Weather Underground web page and create a free Weather Underground account.

Once you have created an account, click on the ‘cog’ icon on the top right of the web page. Then:
* click on the C button to select Celsiusclick on the C button to select Celsius
* click on ‘More Settings’ and select Units: metricclick on ‘More Settings’ and select Units: metric
* click on ‘Save My Preferences’.click on ‘Save My Preferences’.

Now, when you download the data, temperatures will be in Celsius and wind speeds in km/h etc.

---

## 1.1 Removing rogue spaces

One of the problems often encountered with CSV files is rogue spaces before or after data values or column names.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1045.jpg)
__Figure 3__

An image of empty, numbered parking spaces
You learned earlier, in What is a CSV file? , that each value or column name is separated by a comma. However, if you opened ‘London_2014.csv’ in a text editor, you would see that in the row of column names sometimes there are spaces after a comma:

>GMT,Max TemperatureC,Mean TemperatureC,Min TemperatureC,Dew PointC,MeanDew PointC,Min DewpointC,Max Humidity, Mean Humidity, Min Humidity, Max Sea Level PressurehPa, Mean Sea Level PressurehPa, Min Sea Level PressurehPa, Max VisibilityKm, Mean VisibilityKm, Min VisibilitykM, Max Wind SpeedKm/h, Mean Wind SpeedKm/h, Max Gust SpeedKm/h,Precipitationmm, CloudCover, Events,WindDirDegrees



For example, there is a space after the comma between `__Max Humidity__` and `__Mean Humidity__`. This means that when `__read_csv()__` reads the row of column names it will interpret a space after a comma as part of the next column name. So, for example, the column name after `__'Max Humidity'__` will be interpreted as `__' Mean Humidity'__` rather than what was intended, which is `__'Mean Humidity'__`. The ramification of this is that code such as:

`london[['Mean Humidity']]`

will cause a key error (see Selecting a column ), as the column name is confusingly `__' Mean Humidity__` '.

This can easily be rectified by adding another argument to the `__read_csv()__` function:

`skipinitialspace=True`

which will tell `__read_csv()__` to ignore any spaces after a comma:

`__In []:__`




{:.input_area}
```python


london = read_csv('London_2014.csv', skipinitialspace=True)

```


The rogue spaces will no longer be in the dataframe and we can write code such as:

`__In []:__`

`london[['Mean Humidity']].head()`

`__Out[]:__`
<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th></th>
<th>__Mean Humidity__</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">86</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">81</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">76</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">85</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">88</td>
</tr>
</tbody>
</table>
Note that a `__skipinitialspace=True__` argument won’t remove a trailing space at the end of a column name.

Next, find out about extra characters and how to remove them.

## 1.2 Removing extra characters

If you opened London_2014.csv in a text editor once again and looked at the last column name you would see that the name is'WindDirDegrees

'.

What has happened here is that when the dataset was exported from the Weather Underground website an html line break `__(
)__` was added after the line of column headers which `__read_csv()__` has interpreted as the end part of the final column’s name.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1050.jpg)
__Figure 4__

An image of two bouncers in suits standing in a corridor 
In fact, the problem is worse than this, let’s look at some values in the final column:

`__In []:__`

`london[['WindDirDegrees
']].head()`

`__Out[]:__`
<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th></th>
<th>__ WindDirDegrees 
__</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">186
</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">214
</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">219
</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">211
</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">199
</td>
</tr>
</tbody>
</table>
It’s seems there is an html line break at the end of each line. If I opened ‘London_2014.csv’ in a text editor and looked at the ends of all lines in the file this would be confirmed.

Once again I’m not going to edit the CSV file but rather fix the problem in the dataframe. To change `__'WindDirDegrees
'__` to `__'WindDirDegrees'__` all I have to do is use the `__rename()__` method as follows:

`__In []:__`

`
london = london.rename(columns={'WindDirDegrees
':'WindDirDegrees'})
`

Don’t worry about the syntax of the argument for `__rename()__` , just use this example as a template for whenever you need to change the name of a column.

Now I need to get rid of those pesky `__
__` html line breaks from the ends of the values in the `__'WindDirDegrees'__` column, so that they become something sensible. I can do that using the string method `__rstrip()__` which is used to remove characters from the end or ‘rear’ of a string, just like this:

`__In []:__`

`
london['WindDirDegrees'] = london['WindDirDegrees'].str.rstrip('
')
`

Again don’t worry too much about the syntax of the code and simply use it as a template for whenever you need to process a whole column of values stripping characters from the end of each string value.

Let’s display the first few rows of the ' `__WindDirDegrees__` ' to confirm the changes:

`__In []:__`

`london[['WindDirDegrees']].head()`

`__Out[]:__`
<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th></th>
<th>__WindDirDegrees__</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">186</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">214</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">219</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">211</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">199</td>
</tr>
</tbody>
</table>

## 1.3 Missing values

As you heard in the video at the start of the week, missing values (also called null values) are one of the reasons to clean data.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1051.jpg)
__Figure 5__

An image of a girl with the last piece of a jigsaw puzzle 
Finding missing values in a particular column can be done with the column method `__isnull()__` , like this:

`__In []:__`

`london['Events'].isnull()`

The above code returns a series of Boolean values, where `__True__` indicates that the corresponding row in the `__'Events'__` column is missing a value and `__False__` indicates the presence of a value. Here are the last few rows from the series:




{:.input_area}
```python

...
360 False
361 True
362 True
363 True
364 False
Name: Events, dtype: bool
```


If, as you did with the comparison expressions, you put this code within square brackets after the dataframe’s name, it will return a new dataframe consisting of all the rows without recorded events (rain, fog, thunderstorm, etc.):

`__In []:__`

`london[london['Events'].isnull()]`

As you will see in Exercise 4 of the exercise notebook, this will return a new dataframe with 114 rows, showing that more than one in three days had no particular event recorded. If you scroll the table to the right, you will see that all values in the `__'Events'__` column are marked `__NaN__` , which stands for ‘Not a Number’, but is also used to mark non-numeric missing values, like in this case (events are strings, not numbers).

Once you know how much and where data is missing, you have to decide what to do: ignore those rows? Replace with a fixed value? Replace with a computed value, like the mean?

In this case, only the first two options are possible. The method call `__london.dropna()__` will drop (remove) all rows that have a missing (non-available) value somewhere, returning a new dataframe. This will therefore also remove rows that have missing values in other columns.

The column method `__fillna()__` will replace all non-available values with the value given as argument. For this case, each NaN could be replaced by the empty string.

`__In []:__`




{:.input_area}
```python

london['Events'] = london['Events'].fillna('')
ondon[london['Events'].isnull()]
```


The second line above will now show an empty dataframe, because there are no longer missing values in the events column.

As a final note on missing values, pandas ignores them when computing numeric statistics, i.e. you don’t have to remove missing values before applying `__sum(), median()__` and other similar methods.

Learn about checking data types of each column in the next section.

## 1.4 Changing the value types of columns

The function `__read_csv()__` may, for many reasons, wrongly interpret the data type of the values in a column, so when cleaning data it’s important to check the data types of each column are what is expected, and if necessary change them.

The data type of every column in a dataframe can be determined by looking at the dataframe’s `__dtypes__` attribute, like this:

`__In []:__`

`london.dtypes`

`__Out[]:__`




{:.input_area}
```python

GMT object
Max TemperatureC int64
Mean TemperatureC int64
Min TemperatureC int64
Dew PointC int64
MeanDew PointC int64
Min DewpointC int64
Max Humidity int64
Mean Humidity int64
Min Humidity int64
Max Sea Level PressurehPa int64
Mean Sea Level PressurehPa int64
Min Sea Level PressurehPa int64
Max VisibilityKm int64
Mean VisibilityKm int64
Min VisibilitykM int64
Max Wind SpeedKm/h int64
Mean Wind SpeedKm/h int64
Max Gust SpeedKm/h float64
Precipitationmm float64
CloudCover float64
Events object
WindDirDegrees object
dtype: object
```


In the above output, you can see the column names to the left and to the right the data types of the values in those columns.
* is the pandas data type for whole numbers such as`__int64__` is the pandas data type for whole numbers such as `__55__` or `__2356__`
* is the pandas data type for decimal numbers such as`__float64__` is the pandas data type for decimal numbers such as `__55.25__` or `__2356.00__`
* is the pandas data type for strings such as`__object__` is the pandas data type for strings such as `__'hello world'__` or `__'rain'__`

Most of the column data types seem fine, however two are of concern, `__'GMT'__` and `__'WindDirDegrees'__` , both of which are of type `__object.__` Let’s take a look at `__'WindDirDegrees'__` first.

---

###  Changing the data type of the 'WindDirDegrees' column

The `__read_csv()__` method has interpreted the values in the `__'WindDirDegrees'__` column as strings (type `__object__` ). This is because in the CSV file the values in that column had all been suffixed with that html line break string `__
__` so `__read_csv()__` had no alternative but to interpret the values as strings.

The values in the `__'WindDirDegrees'__` column are meant to represent wind direction in terms of degrees from true north (360) and meteorologists always define the wind direction as the direction the wind is coming from. So if you stand so that the wind is blowing directly into your face, the direction you are facing names the wind, so a westerly wind is reported as 270 degrees. The compass rose shown below should make this clearer:

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1007.jpg)
__Figure 6__ A compass rose 

We need to be able to make queries such as ‘Get and display the rows where the wind direction is greater than 350 degrees’. To do this we need to change the data type of the ‘WindDirDegrees’ column from object to type `__int64__`. We can do that by using the `__astype()__` method like this:

`__In []:__`

`
london['WindDirDegrees'] = london['WindDirDegrees'].astype('int64')
`

Now all the values in the `__'WindDirDegrees'__` column are of type `__int64__` and we can make our query:

`__In []:__`

`london[london['WindDirDegrees'] &gt; 350]`

`__Out[]:__`

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1008.jpg)
__Figure 7__

Rows from the london dataframe where the value in the WindDirDegrees column is greater than 350. Note that the WindDirDegrees column is not shown as it is on the far right of the table and only the first few columns are shown due to the limitation of page width. 
* Note that the `__'WindDirDegrees'__` column is on the far right of the table and the right of the table has been cropped to fit on the page. *

---

---

### Changing the data type of the ‘GMT’ column

Recall that I noted that the `__'GMT'__` column was of type `__object__` , the type pandas uses for strings.

The `__'GMT'__` column is supposed to represent dates. It would be helpful for the date values not to be strings to make it possible to make queries of the data such as ‘Return the row where the date is 4 June 2014’.

Pandas has a function called `__to_datetime()__` which can convert a column of `__object__` (string) values such as those in the `__'GMT'__` column into values of a proper date type called `__datetime64__
,
` just like this:

`__In []:__`




{:.input_area}
```python

london['GMT'] = to_datetime(london['GMT'])

#Then display the types of all the columns again so we

#can check the changes have been made.
london.dtypes
```


`__Out[]:__`




{:.input_area}
```python

GMT datetime64[ns]
Max TemperatureC int64
Mean TemperatureC int64
Min TemperatureC int64
Dew PointC int64
MeanDew PointC int64
Min DewpointC int64
Max Humidity int64
Mean Humidity int64
Min Humidity int64
Max Sea Level PressurehPa int64
Mean Sea Level PressurehPa int64
Min Sea Level PressurehPa int64
Max VisibilityKm int64
Mean VisibilityKm int64
Min VisibilitykM int64
Max Wind SpeedKm/h int64
Mean Wind SpeedKm/h int64
Max Gust SpeedKm/h float64
Precipitationmm float64
CloudCover float64
Events object
WindDirDegrees int64
dtype: object
```


From the above output, we can confirm that the `__'WindDirDegrees'__` column type has been changed from `__object__` to `__int64__` and that the `__'GMT'__` column type has been changed from `__object__` to `__datetime64__`.

To make queries such as ‘Return the row where the date is 4 June 2014’ you’ll need to be able to create a `__datetime64__` value to represent June 4 2014. It cannot be:

`london[london['GMT'] == '2014-1-3']`

because ‘2014-1-3’ is a string and the values in the ‘GMT’ column are of type `__datetime64__`. Instead you must create a `__datetime64__` value using `__thedatetime()__` function like this:

`datetime(2014, 6, 4)`

In the function call above, the first integer argument is the year, the second the month and the third the day.

Let’s try the function out by executing the code to ‘Return the row where the date is 4 June 2014’:

`__In []:__`

`london[london['GMT'] == datetime(2014, 6, 4)]`

`__Out[]:__`

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1009.jpg)
__Figure 8__

The row from the london dataframe where the date is 4 June 2014. Note that only the first few columns are shown due to the limitation of page width. 
* Note that the right side of the table has been cropped to fit on the page. *

You can also now make more complex queries involving dates such as ‘Return all the rows where the date is between 8 December 2014 and 12 December 2014’, like this:

`__In []:__`

c




{:.input_area}
```python

london[(london['GMT'] >= datetime(2014, 12, 8)) 
    & (london['GMT'] <= datetime(2014, 12, 12))]
```


`__Out[]:__`

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1010.jpg)
__Figure 9__

The rows from the london dataframe where the date is between 8 December 2014 and 12 December 2014 (inclusive). Note that only the first few columns are shown due to the limitation of page width. 
*Note that the right side of the table has been cropped to fit on the page. *

### Exercise 4 Display rows from dataframe

#### Question

Now try Exercise 4 in the Exercise notebook 2.

If you’re using Anaconda instead of CoCalc, remember that to open the notebook you’ll need to navigate to the notebook using Jupyter.

Once the notebook is open, run the existing code in the notebook before you start the exercise. When you’ve completed the exercise, save the notebook. If you need a quick reminder of how to use Jupyter, watch again the video in Week 1 Exercise 1.


---

