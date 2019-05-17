---
redirect_from:
  - "/testdir/test-9-6"
interact_link: content/testdir/test_9_6.ipynb
kernel_name: 
has_widgets: false
title: 'test_9_6'
prev_page:
  url: /testdir/test_9_5
  title: 'test_9_5'
next_page:
  url: /testdir/test_10_3
  title: 'test_10_3.md'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# 4 Summary


![](https://www.open.edu/openlearn/ocw/pluginfile.php/1393338/mod_oucontent/oucontent/71687/ou_futurelearn_learn_to_code_fig_1076_3d.jpg)
__Figure 7__

An image of python code on a computer screen.
This week you used Jupyter notebooks to write and execute simple programs with Python and the pandas module. You've learned how to:
* load a table from an Excel fileload a table from an Excel file
* select a column, and compute some simple statistics (like the total, minimum and median) about it.select a column, and compute some simple statistics (like the total, minimum and median) about it. 
* create a new column with values calculated from other columnscreate a new column with values calculated from other columns
* sort a table by one of its columns.sort a table by one of its columns.

Next week you will learn further ways to manipulate dataframes, in particular to clean data. You will also produce your first data chart, showing variations of values over time.

---

### Futher reading
[WHO population – data by country (2013)](http://apps.who.int/gho/data/node.main.POP107?lang=en)[ WHO mortality and prevalence – data by country (2007 – present) ](http://apps.who.int/gho/data/node.country)
---

## 4.1 Week 1 and 2 glossary

Here are alphabetical lists, for quick look up, of what this week introduced.

---

### Programming and data analysis concepts

An __assignment__ is a statement of the form 



{:.input_area}
```
__variable = expression__
```


 . It evaluates the expression and stores its value in the variable. The variable is created if it doesn’t exist. Each assignment is written on its own line.

__CamelCase__ is a naming style in which names made of various words have each word capitalized, except possibly the first.

A __comment__ is a note about the code. It starts with the hash sign (#) and goes until the end of the line.

A __dataframe__ is the pandas representation of a table.

An __expression__ is a fragment of code that can be __evaluated__ , i.e. that has a value, like a variable name.

A __file not found__ error occurs if the computer can’t find the given file, e.g. because the name is misspelled or because it’s in another folder.

A __function__ takes zero or more __arguments__ (values) and __returns__ (produces) a value.

A __function call__ is an expression of the form 



{:.input_area}
```
__functionName(argument1, argument2, …).__
```


An __import statement__ of the form 



{:.input_area}
```
__from module import__
```


 * loads all the code from the given module.

The __maximum__ and __minimum__ of a set of values is the largest and smallest value, respectively.

The __mean__ of a set of numbers is the sum of those numbers divided by how many there are.

The __median__ of a set of numbers is the number in the middle, i.e. half of the numbers are below the median and half are above.

A __method__ is a function that can only be called in a certain context, like a dataframe or a column.

A __method call__ is an expression of the form 



{:.input_area}
```
__context.methodName(argument1, argument2, ...).__
```


A __module__ is a package of various pieces of code that can be used individually.

A __name__ is a case-sensitive sequence of letters, digits and underscores. Names cannot start with a digit. Function, variable and module names usually start with lowercase.

A __name error__ occurs if the computer doesn’t recognize a name, e.g. if it was misspelled.

An __operator__ is a symbol that represents some operation on one or two expressions, e.g. the four basic arithmetic operators.

The __range__ of a set of values is the difference between the maximum and the minimum.

A __reserved__ word cannot be used as a name. Jupyter shows reserved words in green boldface.

A __statement__ is a command for the computer to do something, e.g. to assign a value or to import some code.

A __string__ is a verbatim piece of text, surrounded by quotes. Jupyter shows strings in red.

A __syntax error__ occurs if the computer can’t understand the code because it is not in the expected form, e.g. if a reserved word is used instead of a name or some punctuation is missing.

A __variable__ is a named storage for values.

---

---

### Reserved words
* 



{:.input_area}
```
__from__
```


* 



{:.input_area}
```
__import__
```


---

---

### Functions and methods





{:.input_area}
```
__max(value1, value2, …)__
```


 returns the maximum of the given values.





{:.input_area}
```
__column.max()__
```


 returns the maximum value in the column.





{:.input_area}
```
__min(value1, value2, …)__
```


 returns the minimum of the given values.





{:.input_area}
```
__column.min()__
```


 returns the minimum value in the column.





{:.input_area}
```
__column.mean()__
```


 returns the mean of the values in the column.





{:.input_area}
```
__column.median()__
```


 returns the median of the values in the column.





{:.input_area}
```
__column.sum()__
```


 returns the total of the values in the column.





{:.input_area}
```
__dataFrame.sort_values(columnName)__
```


 takes a string with a column’s name and returns a new dataframe, in which rows are sorted in ascending order according to the values in the given column.





{:.input_area}
```
__read_excel(fileName)__
```


 takes a string with an Excel file name, reads the file, and returns a dataframe representing the table in the file.

---

