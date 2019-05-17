---
redirect_from:
  - "/testdir/test-10-4"
interact_link: content/testdir/test_10_4.ipynb
kernel_name: python3
has_widgets: false
title: 'test_10_4'
prev_page:
  url: /testdir/test_10_3
  title: 'test_10_3.md'
next_page:
  url: /testdir/test_10_5
  title: 'test_10_5'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# 1 Weather data

This week you will be looking at investigating historic weather data.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1039.jpg)
__Figure 1__

An image of filter like diagonal strips across various skies such as an orange sunset, a storm and a clear blue sky
Of course, such data is hugely important for research into the large-scale, long-term shift in our planet’s weather patterns and average temperatures – climate change. However, such data is also incredibly useful for more mundane planning purposes. To demonstrate the learning this week, I, Rob Griffiths, will be using historic weather data to try and plan a summer holiday in the UK. You’ll use the data too and get a chance to work on your own project at the end of the week.

The dataset we’ll use to do this will come from the [Weather Underground](http://www.wunderground.com/), which creates weather forecasts from data sent to them by a worldwide network of over 100,000 weather enthusiasts who have personal weather stations on their house or in their garden.

In addition to creating weather forecasts from that data, the Weather Underground also keeps that data as historic weather records allowing members of the public to download weather datasets for a particular time period and location. These datasets are downloaded as CSV files, explained in the next step.

Datasets are rarely ‘clean’ and fit for purpose, so it will be necessary to clean up the data and ‘mould it’ for your purposes. You will then learn how to visualise data by creating graphs using the 



{:.input_area}
```python
__plot()__
```


 function.

## 1.1 What is a CSV file?

A CSV file is a plain text file that is used to hold tabular data. The acronym CSV is short for ‘comma-separated values’.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1036.jpg)
__Figure 2__

An image of many pins marking various countries on a globe
Take a look at the first few lines of a CSV file that holds the same data as the Excel file ‘WHO POP TB all.xls’ that you encountered in Week 2:




{:.input_area}
```python

Country,Population (1000s),TB deaths
Afghanistan,30552,13000.0
Albania,3173,20.0
Algeria,39208,5100.0
Andorra,79,0.26 
Angola,21472,6900.0
Antigua and Barbuda,90,1.2
Argentina,41446,570.0 
Armenia,2977,170.0
```


Notice that the first line is a row of column names. The subsequent lines are rows of actual data that correspond to the column names. The row of column names is optional, but it is helpful in understanding the data in the following lines and making sure the right values fall in the right place. In this example, the first value on every row must be a string representing a country’s name, the second value is an integer representing that country’s population (in 1000s) and the third value is a decimal representing the number of deaths due to TB. Note that the third value is a decimal (like 0.26 deaths for Andorra) and not an integer because it is an estimate obtained from statistical processing of collected data.

Note that each value or column name is separated by a comma but actually any character can be used to separate values in a CSV file, including spaces and tabs etc., hence CSV can also stand for ‘character-separated values’.

Because CSV files are in plain-text it makes the data easy to import into any spreadsheet program, database or pandas dataframe.

Before anything can be done with a CSV file with pandas, the following import statement must be executed:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
from pandas import *
```


As you learned in Week 2, the import statement loads into memory all the code in the pandas module.

To read a CSV file into a dataframe, the pandas function 



{:.input_area}
```python
__read_csv()__
```


 needs to be called.





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df = read_csv('WHO POP TB all.csv')
```


The above code creates a dataframe from the data in the file 



{:.input_area}
```python
__WHO POP TB__
```







{:.input_area}
```python
__all.csv__
```


 and assigns it to the variable 



{:.input_area}
```python
__df__
```


. This is the simplest usage of the 



{:.input_area}
```python
__read_csv()__
```


 function, just using a single argument, a string that holds the name of the CSV file.

However the function can take many additional arguments (some of which you’ll use later), which determine how the file is to be read.

In the next step, find out about dataframes and the ‘dot’ notation.

## 1.2 Dataframes and the ‘dot’ notation

In Week 2 you learned that dataframes have methods, which are like functions, that can only be called in the context of a dataframe.

For example, because the TB deaths dataframe 



{:.input_area}
```python
__df __
```


has a column named ‘Country’, the 



{:.input_area}
```python
__sort_values()__
```


 method can be called like this:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.sort_values('Country')
```


Because there is variable name, followed by a dot, followed by the method, this is called __dot notation__. Methods are said to be a property of a dataframe. In addition to methods, dataframes have another property – attributes.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1040.jpg)
__Figure 3__

A multi-coloured image of many different sized circles. They could be described as bubbles
---

### Attributes

A dataframe attribute is like a variable that can only be accessed in the context of a dataframe. One such attribute is 



{:.input_area}
```python
__columns __
```


which holds a dataframe’s column names.

So the expression 



{:.input_area}
```python
__df.columns__
```


 evaluates to the value of the 



{:.input_area}
```python
__columns __
```


attribute inside the dataframe 



{:.input_area}
```python
__df__
```


. The following code will get and display the names of the columns in the dataframe 



{:.input_area}
```python
__df:__
```









{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.columns
```









{:.input_area}
```python
__Out[]:__
```








{:.input_area}
```python

Index(['Country', 'Population (1000s)', 'TB deaths'],
dtype='object')
```


---

## 1.3 Getting and displaying dataframe rows

Dataframes can have hundreds or thousands of rows, so it is not practical to display a whole dataframe.

However, there are a number of dataframe attributes and methods that allow you to get and display either a single row or a number of rows at a time. Three of the most useful methods are:



{:.input_area}
```python
__ iloc()__
```


, 



{:.input_area}
```python
__head()__
```


 and 



{:.input_area}
```python
__tail()__
```


. Note that to distinguish methods and attributes, we write 



{:.input_area}
```python
()
```


 after a method’s name.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1041.jpg)
__Figure 4__

An image of a data algorithm 
---

### The iloc attribute

A dataframe has a default integer index for its rows, which starts at 0 (zero). You can get and display any single row in a dataframe by using the



{:.input_area}
```python
__iloc__
```


 attribute with the index of the row you want to access as its argument. For example, the following code will get and display the first row of data in the dataframe 



{:.input_area}
```python
__df__
```


, which is at index 0:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.iloc[0]
```









{:.input_area}
```python
__Out[]:__
```








{:.input_area}
```python

Country Afghanistan
Population (1000s) 30552
TB deaths 13000
Name: 0, dtype: object
```


Similarly, the following code will get and display the third row of data in the dataframe 



{:.input_area}
```python
__df__
```


, which is at index 2:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.iloc[2]
```









{:.input_area}
```python
__Out[]:__
```








{:.input_area}
```python

Country Algeria
Population (1000s) 39208
TB deaths 5100.0
Name: 0, dtype: object
```


---

---

### The head() method

The first few rows of a dataframe can be printed out with the 



{:.input_area}
```python
__head()__
```


 method.

You can tell 



{:.input_area}
```python
__head()__
```


 is a method, rather than an attribute such as 



{:.input_area}
```python
__columns__
```


, because of the parentheses (round brackets) after the property name.

If you don’t give any argument, i.e. don’t put any number within those parentheses, the default behaviour is to return the first five rows of the dataframe. If you give an argument, it will print that number of rows (starting from the row indexed by 0).

For example, executing the following code will get and display the first five rows in the dataframe 



{:.input_area}
```python
__df__
```


.





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.head()
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>Country</th>
<th>Population (1000s)</th>
<th>TB deaths</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">Afghanistan</td>
<td class="highlight_" rowspan="" colspan="">30552</td>
<td class="highlight_" rowspan="" colspan="">13000.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">Albania</td>
<td class="highlight_" rowspan="" colspan="">3173</td>
<td class="highlight_" rowspan="" colspan="">20.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">Algeria</td>
<td class="highlight_" rowspan="" colspan="">39208</td>
<td class="highlight_" rowspan="" colspan="">5100.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">Andorra</td>
<td class="highlight_" rowspan="" colspan="">79</td>
<td class="highlight_" rowspan="" colspan="">0.26</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">Angola</td>
<td class="highlight_" rowspan="" colspan="">21472</td>
<td class="highlight_" rowspan="" colspan="">6900.00</td>
</tr>
</tbody>
</table>
And, executing the following code will get and display the first seven rows in the dataframe 



{:.input_area}
```python
__df.__
```









{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.head(7)
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>Country</th>
<th>Population (1000s)</th>
<th>TB deaths</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">Afghanistan</td>
<td class="highlight_" rowspan="" colspan="">30552</td>
<td class="highlight_" rowspan="" colspan="">13000.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">Albania</td>
<td class="highlight_" rowspan="" colspan="">3173</td>
<td class="highlight_" rowspan="" colspan="">20.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">Algeria</td>
<td class="highlight_" rowspan="" colspan="">39208</td>
<td class="highlight_" rowspan="" colspan="">5100.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">Andorra</td>
<td class="highlight_" rowspan="" colspan="">79</td>
<td class="highlight_" rowspan="" colspan="">0.26</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">Angola</td>
<td class="highlight_" rowspan="" colspan="">21472</td>
<td class="highlight_" rowspan="" colspan="">6900.00</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">5</td>
<td class="highlight_" rowspan="" colspan="">Antigua and Barbuda</td>
<td class="highlight_" rowspan="" colspan="">90</td>
<td class="highlight_" rowspan="" colspan="">1.20</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">6</td>
<td class="highlight_" rowspan="" colspan="">Argentina</td>
<td class="highlight_" rowspan="" colspan="">41446</td>
<td class="highlight_" rowspan="" colspan="">570.00</td>
</tr>
</tbody>
</table>
---

---

### The tail() method

The 



{:.input_area}
```python
__tail()__
```


 method is similar to the 



{:.input_area}
```python
__head()__
```


 method.

If no argument is given, the last five rows of the dataframe are returned, otherwise the number of rows returned is dependent on the argument, just like for the 



{:.input_area}
```python
__head()__
```


 method.





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df.tail()
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>Country</th>
<th>Population (1000s)</th>
<th>TB deaths</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">189</td>
<td class="highlight_" rowspan="" colspan="">Venezuela (Bolivarian Republic of)</td>
<td class="highlight_" rowspan="" colspan="">30405</td>
<td class="highlight_" rowspan="" colspan="">480</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">190</td>
<td class="highlight_" rowspan="" colspan="">Viet Nam</td>
<td class="highlight_" rowspan="" colspan="">91680</td>
<td class="highlight_" rowspan="" colspan="">17000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">191</td>
<td class="highlight_" rowspan="" colspan="">Yemen</td>
<td class="highlight_" rowspan="" colspan="">24407</td>
<td class="highlight_" rowspan="" colspan="">990</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">192</td>
<td class="highlight_" rowspan="" colspan="">Zambia</td>
<td class="highlight_" rowspan="" colspan="">14539</td>
<td class="highlight_" rowspan="" colspan="">3600</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">193</td>
<td class="highlight_" rowspan="" colspan="">Zimbabwe</td>
<td class="highlight_" rowspan="" colspan="">14150</td>
<td class="highlight_" rowspan="" colspan="">5700</td>
</tr>
</tbody>
</table>
---

## 1.4 Getting and displaying dataframe columns

You learned in Week 2 that you can get and display a single column of a dataframe by putting the name of the column (in quotes) within square brackets immediately after the dataframe’s name.

For example, like this:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df['TB deaths']
```


You then get output like this:





{:.input_area}
```python
__Out[]:__
```








{:.input_area}
```python

0    13000.00
1       20.00
2     5100.00
3        0.26
4     6900.00
5        1.20
6      570.00
...
```


Notice that although there is an index, there is no column heading. This is because what is returned is not a new dataframe with a single column but an example of the 



{:.input_area}
```python
__Series__
```


 data type.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1042.jpg)
__Figure 5__

An perspective image of the isle between many data storage towers. The floor and the storage units are lit up.
---

### Each column in a dataframe is an example of a series

The 



{:.input_area}
```python
__Series__
```


 data type is a collection of values with an integer index that starts from zero. In addition, the 



{:.input_area}
```python
__Series__
```


 data type has many of the same methods and attributes as the 



{:.input_area}
```python
__DataFrame__
```


 data type, so you can still execute code like:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df['TB deaths'].head()
```









{:.input_area}
```python
__Out[]:__
```








{:.input_area}
```python

0    13000.00
1       20.00
2     5100.00
3        0.26
4     6900.00
Name: TB deaths, dtype: float64
```


And





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df['TB deaths'].iloc[2]
```









{:.input_area}
```python
__Out[]:__
```









{:.input_area}
```python
5100.00
```


However, pandas does provide a mechanism for you to get and display one or more selected columns as a new dataframe in its own right. To do this you need to use a __list__. A list in Python consists of one or more items separated by commas and enclosed within square brackets, for example 



{:.input_area}
```python
__['Country']__
```


 or



{:.input_area}
```python
__ ['Country', 'Population (1000s)']__
```


. This list is then put within outer square brackets immediately after the dataframe’s name, like this:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df[['Country']].head()
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>__Country__</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">Afghanistan</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">Albania</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">Algeria</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">Andorra</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">Angola</td>
</tr>
</tbody>
</table>
Note that the column is now named. The expression



{:.input_area}
```python
__ df[['Country']]__
```


(with two square brackets) evaluates to a new dataframe (which happens to have a single column) rather than a series.

To get a new dataframe with multiple columns you just need to put more column names in the list, like this:





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df[['Country', 'Population (1000s)']].head()
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>__Country__</th>
<th>__Population (1000s)__</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">0</td>
<td class="highlight_" rowspan="" colspan="">Afghanistan</td>
<td class="highlight_" rowspan="" colspan="">30552</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">1</td>
<td class="highlight_" rowspan="" colspan="">Albania</td>
<td class="highlight_" rowspan="" colspan="">3173</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">2</td>
<td class="highlight_" rowspan="" colspan="">Algeria</td>
<td class="highlight_" rowspan="" colspan="">39208</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">3</td>
<td class="highlight_" rowspan="" colspan="">Andorra</td>
<td class="highlight_" rowspan="" colspan="">79</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">4</td>
<td class="highlight_" rowspan="" colspan="">Angola</td>
<td class="highlight_" rowspan="" colspan="">21472</td>
</tr>
</tbody>
</table>
The code has returned a new dataframe with just the 



{:.input_area}
```python
__'Country'__
```


 and 



{:.input_area}
```python
__'Population (1000s)’__
```


 columns.

### Exercise 1 Dataframes and CSV files

#### Question

Now that you’ve learned about CSV files and more about pandas you are ready to complete Exercise 1 in the exercise notebook 2.

Open the exercise 2 notebook and the data file you used last week WHO POP TB all.csv and save it in the folder you created in Week 1.

If you’re using Anaconda instead of CoCalc, remember that to open the notebook you’ll need to navigate to the notebook using Jupyter. Once it’s open, run the existing code in the notebook before you start the exercise. When you’ve completed the exercise, save the notebook. If you need a quick reminder of how to use Jupyter watch again the video in Week 1 Exercise 1.


---

## 1.5 Comparison operators

In Expressions, you learned that Python has arithmetic operators: +, /, - and * and that expressions such as 5 + 2 evaluate to a value (in this case the number 7).

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1043.jpg)
__Figure 6__

An illustration of two girls holding up signs. One sign says, 'YES', the other says, 'NO'.
Python also has what are called comparison operators, these are:




{:.input_area}
```python

==    equals
!=    not equal
<     less than
>     greater than
<=    less than or equal to 
>=    greater than or equal to
```


Expressions involving these operators always evaluate to a Boolean value, that is 



{:.input_area}
```python
__True__
```


 or 



{:.input_area}
```python
__False__
```


. Here are some examples:




{:.input_area}
```python

2 = = 2      evaluates to True
2 + 2 = = 5  evaluates to False
2 != 1 + 1   evaluates to False
45 < 50      evaluates to True
20 > 30      evaluates to False
100 <= 100   evaluates to True
101 >= 100   evaluates to True
```


The comparison operators can be used with other types of data, not just numbers. Used with strings they compare using alphabetical order. For example:





{:.input_area}
```python
'aardvark' &lt; 'zebra' evaluates to True
```


In Calculating over columns you saw that when applied to whole columns, the arithmetic operators did the calculations row by row. Similarly, an expression like 



{:.input_area}
```python
__df['Country'] &gt;= 'K'__
```


 will compare the country names, row by row, against the string 'K' and record whether the result is 



{:.input_area}
```python
__True__
```


 or 



{:.input_area}
```python
__False__
```


 in a series like this:




{:.input_area}
```python

0    False
1    False
2    False
3    False
4    False
5    False
...
Name: Country, dtype: bool 
```


If such an expression is put within square brackets immediately after a dataframe’s name, a new dataframe is obtained with only those rows where the result is 



{:.input_area}
```python
__True__
```


. So:





{:.input_area}
```python
df[df['Country'] &gt;= 'K']
```


returns a new dataframe with all the columns of 



{:.input_area}
```python
__df __
```


but with only the rows corresponding to countries starting with K or a letter later in the alphabet.

As another example, to see the data for countries with over 80 million inhabitants, the following code will return and display a new dataframe with all the columns of 



{:.input_area}
```python
__df__
```


 but with only the rows where it is 



{:.input_area}
```python
__True__
```


 that the value in the 



{:.input_area}
```python
__'Population (1000s)'__
```


 column is greater than 



{:.input_area}
```python
__80000:__
```









{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df[df['Population (1000s)'] &gt; 80000]
```









{:.input_area}
```python
__Out[]:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>Country</th>
<th>Population (1000s)</th>
<th>TB deaths</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">13</td>
<td class="highlight_" rowspan="" colspan="">Bangladesh</td>
<td class="highlight_" rowspan="" colspan="">156595</td>
<td class="highlight_" rowspan="" colspan="">80000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">23</td>
<td class="highlight_" rowspan="" colspan="">Brazil</td>
<td class="highlight_" rowspan="" colspan="">200362</td>
<td class="highlight_" rowspan="" colspan="">4400</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">36</td>
<td class="highlight_" rowspan="" colspan="">China</td>
<td class="highlight_" rowspan="" colspan="">1393337</td>
<td class="highlight_" rowspan="" colspan="">41000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">53</td>
<td class="highlight_" rowspan="" colspan="">Egypt</td>
<td class="highlight_" rowspan="" colspan="">82056</td>
<td class="highlight_" rowspan="" colspan="">550</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">58</td>
<td class="highlight_" rowspan="" colspan="">Ethiopia</td>
<td class="highlight_" rowspan="" colspan="">94101</td>
<td class="highlight_" rowspan="" colspan="">30000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">65</td>
<td class="highlight_" rowspan="" colspan="">Germany</td>
<td class="highlight_" rowspan="" colspan="">82727</td>
<td class="highlight_" rowspan="" colspan="">300</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">77</td>
<td class="highlight_" rowspan="" colspan="">India</td>
<td class="highlight_" rowspan="" colspan="">1252140</td>
<td class="highlight_" rowspan="" colspan="">240000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">78</td>
<td class="highlight_" rowspan="" colspan="">Indonesia</td>
<td class="highlight_" rowspan="" colspan="">249866</td>
<td class="highlight_" rowspan="" colspan="">64000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">85</td>
<td class="highlight_" rowspan="" colspan="">Japan</td>
<td class="highlight_" rowspan="" colspan="">127144</td>
<td class="highlight_" rowspan="" colspan="">2100</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">109</td>
<td class="highlight_" rowspan="" colspan="">Mexico</td>
<td class="highlight_" rowspan="" colspan="">122332</td>
<td class="highlight_" rowspan="" colspan="">2200</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">124</td>
<td class="highlight_" rowspan="" colspan="">Nigeria</td>
<td class="highlight_" rowspan="" colspan="">173615</td>
<td class="highlight_" rowspan="" colspan="">160000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">128</td>
<td class="highlight_" rowspan="" colspan="">Pakistan</td>
<td class="highlight_" rowspan="" colspan="">182143</td>
<td class="highlight_" rowspan="" colspan="">49000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">134</td>
<td class="highlight_" rowspan="" colspan="">Philippines</td>
<td class="highlight_" rowspan="" colspan="">98394</td>
<td class="highlight_" rowspan="" colspan="">27000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">141</td>
<td class="highlight_" rowspan="" colspan="">Russian Federation</td>
<td class="highlight_" rowspan="" colspan="">142834</td>
<td class="highlight_" rowspan="" colspan="">17000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">185</td>
<td class="highlight_" rowspan="" colspan="">United States of America</td>
<td class="highlight_" rowspan="" colspan="">320051</td>
<td class="highlight_" rowspan="" colspan="">490</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">190</td>
<td class="highlight_" rowspan="" colspan="">Viet Nam</td>
<td class="highlight_" rowspan="" colspan="">91680</td>
<td class="highlight_" rowspan="" colspan="">17000</td>
</tr>
</tbody>
</table>

### Exercise 2 Comparison operators

#### Question

You are ready to complete Exercise 2 in the Exercise notebook 2.

Remember to run the existing code in the notebook before you start the exercise. When you’ve completed the exercise, save the notebook. 



## 1.6 Bitwise operators

To build more complicated expressions involving column comparisons, there are two bitwise operators.

![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1044.jpg)
__Figure 7__

An image of someone constructing a building from wooden blocks
The 



{:.input_area}
```python
__&amp;__
```


 operator means ‘and’ and the | operator (vertical bar, not uppercase letter ‘i’) means ‘or’. So, for example the expression:




{:.input_area}
```python

(df['Country'] >= 'Latvia') & (df['Country'] <= 'Sweden')
```


will evaluate to a series containing Boolean values where the values are



{:.input_area}
```python
__True__
```


 only if the equivalent rows in the dataframe contain the countries ‘



{:.input_area}
```python
__Latvia__
```


’ to ‘



{:.input_area}
```python
__Sweden__
```


’, inclusive. However, the following expression which uses | (or) rather than &amp; (and):





{:.input_area}
```python
(df['Country'] &gt;= 'Latvia') | (df['Country'] &lt;= 'Sweden')
```


will evaluate to 



{:.input_area}
```python
__True__
```


 for all countries, because every country comes alphabetically after ‘



{:.input_area}
```python
__Latvia__
```


’ (e.g. the ‘UK’) or before '



{:.input_area}
```python
__Sweden__
```


' (e.g. ‘



{:.input_area}
```python
__Brazil__
```


’).

Note the round brackets around each comparison. Without them you will get an error.

The whole expression with multiple comparisons has to be put within 



{:.input_area}
```python
__df[…]__
```


 to get a dataframe with only those rows that match the condition.

As a further example, using different columns, it is relatively easy to find the rows in 



{:.input_area}
```python
__df__
```


 where '



{:.input_area}
```python
__Population (1000s)__
```


' is greater than 



{:.input_area}
```python
__80000__
```


 and where '



{:.input_area}
```python
__TB deaths__
```


' are greater than 



{:.input_area}
```python
10000
```


.





{:.input_area}
```python
__In []:__
```









{:.input_area}
```python
df[(df['Population (1000s)'] &gt; 80000) &amp; (df['TB deaths'] &gt; 10000)]
```









{:.input_area}
```python
__Out []:__
```


<table xmlns:str="http://exslt.org/strings">
<caption></caption>
<tbody>
<tr>
<th> </th>
<th>Country</th>
<th>Population (1000s)</th>
<th>TB deaths</th>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">13</td>
<td class="highlight_" rowspan="" colspan="">Bangladesh</td>
<td class="highlight_" rowspan="" colspan="">156595</td>
<td class="highlight_" rowspan="" colspan="">80000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">36</td>
<td class="highlight_" rowspan="" colspan="">China</td>
<td class="highlight_" rowspan="" colspan="">1393337</td>
<td class="highlight_" rowspan="" colspan="">41000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">58</td>
<td class="highlight_" rowspan="" colspan="">Ethiopia</td>
<td class="highlight_" rowspan="" colspan="">94101</td>
<td class="highlight_" rowspan="" colspan="">30000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">77</td>
<td class="highlight_" rowspan="" colspan="">India</td>
<td class="highlight_" rowspan="" colspan="">1252140</td>
<td class="highlight_" rowspan="" colspan="">240000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">78</td>
<td class="highlight_" rowspan="" colspan="">Indonesia</td>
<td class="highlight_" rowspan="" colspan="">249866</td>
<td class="highlight_" rowspan="" colspan="">64000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">124</td>
<td class="highlight_" rowspan="" colspan="">Nigeria</td>
<td class="highlight_" rowspan="" colspan="">173615</td>
<td class="highlight_" rowspan="" colspan="">160000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">128</td>
<td class="highlight_" rowspan="" colspan="">Pakistan</td>
<td class="highlight_" rowspan="" colspan="">182143</td>
<td class="highlight_" rowspan="" colspan="">49000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">134</td>
<td class="highlight_" rowspan="" colspan="">Philippines</td>
<td class="highlight_" rowspan="" colspan="">98394</td>
<td class="highlight_" rowspan="" colspan="">27000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">141</td>
<td class="highlight_" rowspan="" colspan="">Russian Federation</td>
<td class="highlight_" rowspan="" colspan="">142834</td>
<td class="highlight_" rowspan="" colspan="">17000</td>
</tr>
<tr>
<td class="highlight_" rowspan="" colspan="">190</td>
<td class="highlight_" rowspan="" colspan="">Viet Nam</td>
<td class="highlight_" rowspan="" colspan="">91680</td>
<td class="highlight_" rowspan="" colspan="">17000</td>
</tr>
</tbody>
</table>
These expressions can get long and complicated, making it easy to miss a crucial round or square bracket. In those cases it is best to break up the expression into small steps. The previous example could also be written as:





{:.input_area}
```python
__In []:__
```








{:.input_area}
```python

population = df['Population (1000s)'] 
deaths = df['TB deaths']
df[(population > 80000) & (deaths > 10000)]
```


### Exercise 3 Bitwise operators

#### Question

Complete Exercise 3 in the Exercise notebook 2.



