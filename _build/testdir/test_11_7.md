---
redirect_from:
  - "/testdir/test-11-7"
interact_link: content/testdir/test_11_7.ipynb
kernel_name: 
has_widgets: false
title: 'test_11_7'
prev_page:
  url: /testdir/test_11_6
  title: 'test_11_6'
next_page:
  url: /testdir/test_12_3
  title: 'test_12_3.md'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# 4.1 Week 4 glossary

Here is an alphabetical list of the terms introduced this week, for quick look-up.

---

### Programming and data analysis concepts

The __bitwise operators__



{:.input_area}
```
__&amp;__
```


 (and) and 



{:.input_area}
```
__|__
```


 (or) are used in pandas to build more complicated expressions from two comparison expressions (typically involving column comparisons).

A __Boolean__ has one of two possible values: 



{:.input_area}
```
__True__
```


 or 



{:.input_area}
```
__False__
```


.

A __Comma Separated Values (CSV)__ file is a plain text file that is used to hold tabular data.

A __list__ is a sequence of values, separated by commas, and written within square brackets.

There are six __comparison operators__ that can be used to compare number, string and date values. Expressions composed of these operators evaluate to 



{:.input_area}
```
__True__
```


 or 



{:.input_area}
```
__False__
```


. These operators can also be used to compare every value in a column, row by row, against some number, string or date value. When used in this manner the operators return a series of Boolean values.

The __‘dot’ notation__ is used to access a dataframe’s methods and attributes.

The 



{:.input_area}
```
__Series__
```


 data type is a collection of values with an integer index that starts from zero. Each column in a dataframe is an example of the 



{:.input_area}
```
__Series__
```


 data type. The 



{:.input_area}
```
__Series__
```


 data type has many of the same methods as the 



{:.input_area}
```
__DataFrame__
```


 data type.

The 



{:.input_area}
```
__object__
```


 data type is how pandas represents strings.

The 



{:.input_area}
```
__datetime64__
```


 data type is how pandas represents dates.

The 



{:.input_area}
```
__int64__
```


 data type is how pandas represents integers (whole numbers).

The 



{:.input_area}
```
__float64__
```


 data type is how pandas represents floating point numbers (decimals).

---

---

### Functions and methods





{:.input_area}
```
__asType(aType)__
```


 when applied to a dataframe column, the method changes the data type of each value in that column to the type given by the string 



{:.input_area}
```
__aType__
```


.





{:.input_area}
```
__datetime(yyyy, mm, dd)__
```


 the function takes three arguments, 



{:.input_area}
```
__yyyy__
```


 a four digit integer representing a year, 



{:.input_area}
```
__mm__
```


 a two digit integer representing a month and 



{:.input_area}
```
__dd__
```


 a two digit integer representing a day. From these arguments the function creates and returns a value of 



{:.input_area}
```
__datetime64__
```


.





{:.input_area}
```
__dropna()__
```


 when applied to a dataframe returns a new dataframe without the rows that have at least one missing value.





{:.input_area}
```
__head()__
```


 gets and displays the first five rows of a dataframe. Optionally the method can take an integer argument to specify how many rows (from and including row 0) to get and display.





{:.input_area}
```
__iloc[index]__
```


 gets and displays the row in the dataframe indicated by the integer argument 



{:.input_area}
```
__index__
```


.





{:.input_area}
```
__isnull()__
```


 is a series method that checks which rows in that series have a missing value.





{:.input_area}
```
__fillna(value)__
```


 is a series method that returns a new series in which all missing values have been filled with the given value.





{:.input_area}
```
__plot()__
```


 when applied to a dataframe column of numeric values, the method displays a graph of those values. The x-axis shows the dataframe’s index and the y-axis the range of the column’s values. Before the method is called you first need to execute 



{:.input_area}
```
__%matplotlib inline__
```


.





{:.input_area}
```
__read_csv(csvFile)__
```


 creates a dataframe from the dataset in the CSV file.





{:.input_area}
```
__rename(columns={oldName : newName})__
```


 renames the column 



{:.input_area}
```
__oldName__
```


 to 



{:.input_area}
```
__newName__
```


.





{:.input_area}
```
__str.rstrip(suffix)__
```


 when applied to a dataframe column of string values, the method removes the argument 



{:.input_area}
```
__suffix__
```


 from the end of each string value in the column.





{:.input_area}
```
__tail()__
```


 gets and displays the last five rows of a dataframe. Optionally the method can take an integer argument to specify how many rows (until and including the last row) to get and display.





{:.input_area}
```
__to_datetime(aSeries)__
```


 when applied to a series, typically a column from a dataframe, this function returns a new series in which each value in 



{:.input_area}
```
__aSeries__
```


 has been changed to type 



{:.input_area}
```
__datetime64__
```


.

---

