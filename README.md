![pandas](https://github.com/SzymkowskiDev/pandas-cookbook/blob/master/pandas_logo.png?raw=true)

# Pandas Cookbook 🐼🥘📗
How to perform various data cleaning and manipulation tasks in Pandas.

The project comprises of the following: 
* Jupyter notebook
* this README containing examples 
* and in the future a collection of Kata challanges on CodeWars

The link to the CodeWars Pandas collection will be provided [here](https://www.google.com/search?q=in+progress&tbm=isch&ved=2ahUKEwjQ0rz_7MD4AhWUhP0HHQtoB_QQ2-cCegQIABAA&oq=in+progress&gs_lcp=CgNpbWcQAzIFCAAQgAQyBQgAEIAEMgUIABCABDIECAAQQzIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDoHCCMQ6gIQJzoECCMQJ1DhBlj_E2DxFGgBcAB4AIABXYgBqweSAQIxMpgBAKABAaoBC2d3cy13aXotaW1nsAEKwAEB&sclient=img&ei=Ce-yYpCqMJSJ9u8Pi9CdoA8&bih=802&biw=1706).

## Contents
1. How to run
2. Learning Materials
3. Modules
4. Configurations
5. Cookbook
- 5.1. Creating data types: Series
- 5.2. Creating data types: DataFrame
- 5.3. Loading files into a DataFrame: CSV
- 5.4. Loading files into a DataFrame: JSON
- 5.5. Accessing values: Series
- 5.6. Accessing values: DataFrame
- 5.7. Data Manipulation: Adding rows to a DataFrame
- 5.8. Data Manipulation: Adding columns to a DataFrame
- 5.9. Data Manipulation: From wide to narrow format
- 5.10. Data Manipulation: From narrow to wide format
- 5.11. Data Manipulation: Inner join
- 5.12. Data Manipulation: Left (Outer) join
- 5.13. Data Manipulation: Right (Outer) join
- 5.14. Data Manipulation: Full (Outer) join
6. Warnings / Common Errors / Known Issues
7. Tips
8. Contact
9. License

## 🚀 How to run
1. Download the Jupyter notebook and associated files (my_file.csv and my_json.json)
2. Place the files in the directory where the notebook is located
3. Run the Jupyter notebook

## 🎓 Learning Materials
* Most important source: [Pandas documentation](https://pandas.pydata.org/getting_started.html)
* [Pandas official cheatsheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
* [w3schools Pandas tutorial](https://www.w3schools.com/python/pandas/default.asp)
* [javapoint Pandas tutorial](https://www.javatpoint.com/python-pandas)
* [geeksforgeeks Pandas tutorial](https://www.geeksforgeeks.org/pandas-tutorial/?ref=lbp)
* [kaggle Pandas tutorial](https://www.kaggle.com/learn/pandas)
* [Pandas GitHub repository](https://github.com/pandas-dev/pandas)
* Warning Some API is outdated [4_Tutorial_Pandas_basics_Python.pdf](https://github.com/SzymkowskiDev/pandas-cookbook/blob/master/4_Tutorial_Pandas_basics_Python.pdf)
* Warning Some API is outdated [5_Data_Manipulation_Pandas_Python.pdf](https://github.com/SzymkowskiDev/pandas-cookbook/blob/master/5_Data_Manipulation_Pandas_Python.pdf)

## 📦 Modules
```python
import pandas as pd
```

## ⚙ Configurations
To check the version of Pandas installed run the following in the console:

```python
print(pd.__version__)
```


## 📝 Cookbook

**Creating data types**


🐼 Pandas offers 1-dimensional Series, 2-dimensional DataFrames and used to offer 3-dimensional Panels, that were deprected (since version 0.20.0) in favour of representing 3-D data with a MultiIndex on a DataFrame via the to_frame() method or with the xarray package. Here we deal briefly with Series and extensively with DataFrames.


**1. Creating data types: Series**

* Series is created with the pd.Series() method
* pd.Series() method takes list or dictionary as data argument
* Elements in a series are labelled
* By default labels are integers 0, 1, 2, ...
* To make custom labels you must provide a second "index" argument to the pd.Series() method
* If pd.Series() is fed with a dictioanry, then keys become labels

```python
# Creating data type: Series

# providing a list as data argument, default labels
my_series_list = pd.Series([1, 2, 3])
print(my_series_list) # default labels are integers 0, 1, 2, ...

# providing a list as data argument, custom labels
my_series_list_custom = pd.Series([1, 2, 3], index = ["a", "b", "c"])
print(my_series_list_custom) # to make custom labels provide a second "index argument"

# providing a dictionary as data argument
my_series_dict = pd.Series({"a": 1, "b": 2, "c":3})
print(my_series_dict) # keys become labels
```

**2. Creating data types: DataFrame**

* DataFrame is created using the pd.DatFrame() method
* pd.DataFrame() method takes either Series, dictionary, or another DataFrame as the data argument
* Additionally, some file types like .CSV or .JSON can be imported as a DataFrame (using read_csv() and read_json() functions, more on that later)
* One can create multi-column data frame from Series if it's a dictionary of Series
* When providing a dictionary to pd.DataFrame() the keys become column names
* For multi-row data frame, the values in supplied dictionary must be lists of values
* Apart from the data argument, pd.DatFrame() takes arguments "index" and "columns"
* The optional "index" argument is for labelling rows
* The optional "columns" argument is for selecting which columns from the data argument to include

```python
# data frame from a series
my_df_series = pd.DataFrame(my_series_list)
print(my_df_series) # contains only one column

# data frame from a dictionary of series
my_df_series_2 = pd.DataFrame({"a": my_series_list, "b": my_series_list})
print(my_df_series_2)

# data frame from a dictionary
my_df_dict = pd.DataFrame({"a": [1, 2], "b": [3, 4], "c":[5, 6]})
print(my_df_dict)

# custom row labels with the "index" argument
my_df_labels = pd.DataFrame({"a": [1, 2], "b": [3, 4], "c":[5, 6]}, index = ["first_row", "second_row"])
print(my_df_labels)

# selecting columns with the "colums" argument
my_df_columns = pd.DataFrame({"a": [1, 2], "b": [3, 4], "c":[5, 6]}, columns = ["a", "b"])
print(my_df_columns)
```


**Loading files**


🐼 With Pandas you can read files of multiple types ([full list here](https://pandas.pydata.org/docs/user_guide/io.html)), but in most cases the users needs to read CSV, JSON, XML and MS EXCEL. These 4 are accomplished with: read_csv(), read_json(), read_xml() and read_excel() respectively. Pandas even offers reading of big data fromats such as Apache Parquet, Optimized Row Columnar or Feather (read_parquet(), read_orc() and read_feather()).


**3. Loading files into a DataFrame: CSV**

* .CSV file can be loaded as DataFrame using the pd.read_csv() method
* The most important argument of pd.read_csv() is "filepath"
* A commonly used parameter is "names" used to specify which columns from the csv file to load to the newly created DataFrame
* Other arguments can help with things like specifying headers, separator etc. [other arguments](https://pandas.pydata.org/docs/user_guide/io.html#io-read-csv-table)

```python
# loading a CSV file
my_csv = pd.read_csv("my_file.csv", names = ["A", "B"])
print(my_csv) # The parameter "names" is optional and used to specify which columns to load from the file
```

**4. Loading files into a DataFrame: JSON**

* Reading .JSON files is accomplished with pd.read_json() method
* The first argument is the filepath
* [Other parameters in the documenation](https://pandas.pydata.org/docs/user_guide/io.html#reading-json)

```python
my_json = pd.read_json("my_json.json")
print(my_json)
```

**Accessing**


**5. Accessing values: Series**

* You use square bracket notation to access elements in a Series
* You can access values by referring to its label
```python
x = my_series_list_custom["b"]
print(x)
```
* Or by refering to its position (bearing in mind that Python starts counting at 0)
```python
y = my_series_list_custom[2]
print(y)
```
* The square bracket notation can also be used to set values
```python
my_series_list_custom[0] = 100
print(my_series_list_custom)
```
* You can also use semicolon inside the square brackets to select ranges of values (bearing in mind that end is not included)
```python
z = my_series_list_custom[0:2]
print(z)
```
* You can use the colon without start or end index
```python
# This is what will happen if you won't supply the end index
o = my_series_list_custom[1:]
print(o) # [2, 3]

# This is what will happen if you won't supply the start index
e = my_series_list_custom[:2]
print(e) # [100,2]
```
* You can use logic inside the square bracket notation
```python
b = my_series_list_custom[my_series_list_custom > 50]
print(b) # 100

w = my_series_list_custom[my_series_list_custom  != 100]
print(w) # [2, 3]
```


**6. Accessing values: DataFrame**
* You can use square bracket notation to access columns of a DataFrame
```python
test_df = pd.DataFrame({"col_a": [1, 2, 3], "col_b": ["a", "b", "c"]})

# Output a single column selected by its name
print(test_df["col_a"]) 

# Output multiple columns selected by their name (provide a list of names)
print(test_df[["col_a", "col_b"]]) 
```
* To access rows you need to use .loc[] attribute
```python
# Accessing rows using the .loc[] attribute
print(test_df.loc[0]) # col_a    1, col_b    a
print(test_df.loc[1]) # col_a    2, col_b    b
print(test_df.loc[2]) # col_a    3, col_b    c
# In each case the output is a Series
```
* The .loc[] attribute can be used for setting values as well
```python
test_df.loc[1] = 200
print(test_df)
#    col_a col_b
# 0      1     a
# 1    200   200
# 2      3     c
* To return multiple rows using .loc[] one supplies a list inside the square brackets notation
```python
print(test_df.loc[1:2]) # The output is a DataFrame
```
* If rows in a DataFrame are labelled then you can refer to their names in the .loc[] attribute
```python
print(my_df_labels.loc["second_row"])
```
* QUESTION: What is the difference between .loc[] and .iloc[] attributes?
```python
print(test_df.iloc[0])
print(test_df.loc[0])
# both return:
# col_a    1
# col_b    a
* ANSWER: loc selects rows by their labels, while iloc selects rows by their integer location
```python
# If a DataFrame has custom row names:
#             a  b  c
# first_row   1  3  5
# second_row  2  4  6
# Then to select first row one uses:
print(my_df_labels.loc["first_row"])
print(my_df_labels.iloc[0])
```
* You can supply a second argument the .loc[] attribute to make selection on specified column/columns
```python
print(test_df.loc[0:1, "col_a"])         # Returns a Series
print(test_df.loc[0:1, "col_a":"col_b"]) # Returns a DataFrame
```
* You can perform similar operation using .iloc[] attribute (bearing in mind that the end index is not included)
```python
print(my_df_labels.loc["first_row":"second_row", "a":"b"])
# is the same as:
print(my_df_labels.iloc[0:2, 0:2])
```
* You can use semicolons or provide lists as first two arguments:
```python
print(my_df_labels.iloc[0:2, 0:2])
# is the same as:
print(my_df_labels.iloc[[0, 1], [0, 1]])
```
* Semicolon without start and end means all
```python
print(my_df_labels.iloc[[0, 1], :])
# Which is equivalent to leaving second argument empty
print(my_df_labels.iloc[[0, 1], ])
```
* QUESTION: What are .at[] and .iat[] attributes?
```python
# For a DataFrame
#             a  b  c
# first_row   1  3  5
# second_row  2  4  6

print(my_df_labels.iloc[1, 1])
print(my_df_labels.iat[1, 1])

# Both seemingly return the same value 4

print(type(my_df_labels.iloc[1, 1]))
print(type(my_df_labels.iat[1, 1]))

# Output types is also the same: <class 'numpy.int64'>
```
* ANSWER:  PERFORMANCE. at and iat are very fast versions of loc and iloc [source](https://stackoverflow.com/questions/28757389/pandas-loc-vs-iloc-vs-at-vs-iat)
* While loc and iloc are meant to access multiple values, at and iat are used to access single values from DataFrames
* at takes arguments: row label and column name
```python 
print(my_df_labels.at["second_row", "b"])
```
* iat takes argument: row integer positon, column integer position
```python
print(my_df_labels.iat[1, 1])
```
* You can use logic inside the square bracket notation
```python
print(my_df_labels[my_df_labels["a"] == 2])
print(my_df_labels[my_df_labels > 2])         # Returns DataFrame with NaN where conditon is not met
```


**7. Data Manipulation: Adding rows to a DataFrame**
* You can add a new row by the means of simple assignment:
```python
print(my_df_labels)
#             a  b  c
# first_row   1  3  5
# second_row  2  4  6

my_df_labels.loc["third_row"] = {"a":3, "b":5, "c":7}
print(my_df_labels)
#             a  b  c
# first_row   1  3  5
# second_row  2  4  6
# third_row   3  5  7
```
* To add a new row to a DataFrame use pd.concat() method
* The concat() methods takes a list of data frames as data argument
```python
# You can assign the newly created DatFrame to a new variable
new_df = pd.concat([test_df, n_row])
print(new_df)

# Or you can overwrite the old data frame
test_df = pd.concat([test_df, n_row])
print(test_df)
```

**8. Data Manipulation: Adding columns to a DataFrame**
* You can add columns to a DataFrame using the simple assignment
```python
# For a data frame that looks like this:
n_row = pd.DataFrame({"col_a": [4, 8], "col_b": ["d", "e"]})
# We could do the following:
n_row["col_c"] = pd.DataFrame({"col_c": [True]})
n_row["col_d"] = 100
n_row["col_d"] = [1, 2]
print(n_row)
#     col_a col_b col_c  col_d
# 0      4     d  True      1
# 1      8     e   NaN      2
```


**9. Data Manipulation: From wide to narrow format**

In a wide format we have an identyfing column (e.g. Person) and every variable present in the table gets its own column:
```python
df_wide = pd.DataFrame({"Person": ["Bob", "Alice", "Steve"], "Age": [32, 24, 64], "Weight": [75, 66, 102], "Height": [180, 175, 165]})
#   Person  Age  Weight  Height
# 0    Bob   32      75     180
# 1  Alice   24      66     175
# 2  Steve   64     102     165
```
* Use pd.melt() method to reshape wide data into narrow format
```python
print(pd.melt(df_wide, id_vars = "Person"))
#   Person variable  value
# 0    Bob      Age     32
# 1  Alice      Age     24
# 2  Steve      Age     64
# 3    Bob   Weight     75
# 4  Alice   Weight     66
# 5  Steve   Weight    102
# 6    Bob   Height    180
# 7  Alice   Height    175
# 8  Steve   Height    165
```
* pd.melt() method takes a DataFrame as first argument and id_vars as second argument
* The id_vars serves to identify which column is an identyfing column
* [more on the melt() method in the docs](https://pandas.pydata.org/docs/reference/api/pandas.melt.html)

**10. Data Manipulation: From narrow to wide format**

In a narrow format we have 3 columns: identifying, variable and value:
```python
df_narrow = pd.DataFrame({"Person": ["Bob", "Bob", "Bob", "Alice", "Alice", "Alice", "Steve", "Steve", "Steve"],
                         "Variable": ["Age", "Weigth", "Height", "Age", "Weigth", "Height", "Age", "Weigth", "Height"],
                         "Value": [32, 75, 180, 24, 66, 175, 64, 102, 165]})
#   Person Variable  Value
# 0    Bob      Age     32
# 1    Bob   Weigth     75
# 2    Bob   Height    180
# 3  Alice      Age     24
# 4  Alice   Weigth     66
# 5  Alice   Height    175
# 6  Steve      Age     64
# 7  Steve   Weigth    102
# 8  Steve   Height    165
```
* Use pd.melt() method to reshape a narrow table to a wide table
```python
print(df_narrow.pivot(index = ["Person"], columns = ["Variable"], values = ["Value"]))
#                  Value              
# Variable   Age Height Weigth
# Person                      
# Alice       24    175     66
# Bob         32    180     75
# Steve       64    165    102
```
* The pivot() method takes 3 arguments: index, columns and values
* "index" parameter is the identifying column
* "columns" parameter is the variable that contains names of variables relating to each case
* "value" parameter is for the column with values of each variable of each case

**Standard Joins**
* All the SQL-like joins are performed using the pd.merge() method
* The pd.merge() methods takes three obligatory arguments: table 1, table 2 and how parameter
* The how parameter is to specify the type of join (inner, left, right or outer)

Let's look at the sample data frames:
```python
# table 1
df_1 = pd.DataFrame({"var_1": ["A", "B", "C"], "var_2": [1, 2, 3]})
#   var_1  var_2
# 0     A      1
# 1     B      2
# 2     C      3
```

```python
# table 2
df_2 = pd.DataFrame({"var_1": ["A", "B", "D"], "var_3": [True, False, True]})
#   var_1  var_3
# 0     A   True
# 1     B  False
# 2     D   True
```

* They share only one column name: "var_1"
* For "var_1" they share two values: "A" and "B"

**11. Data Manipulation: Inner join**
* The "on" parameter is optional
```python
print(pd.merge(df_1, df_2, how = "inner", on = "var_1")) # on parameter is optional it asks for a shared variable
#   var_1  var_2  var_3
# 0     A      1   True
# 1     B      2  False
```
* Inner join looks at var_1 in both tables and outputs rows such that values are matched in both tables


**12. Data Manipulation: Left (Outer) join**

```python
print(pd.merge(df_1, df_2, how = "left"))
#   var_1  var_2  var_3
# 0     A      1   True
# 1     B      2  False
# 2     C      3    NaN
```
* The left join will include all the columns and values from table_1
* Where the matching variable (var_1) is not matched in table_2, there for these variables NaN will appear

**13. Data Manipulation: Right (Outer) join**

```python
print(pd.merge(df_1, df_2, how = "right"))
#   var_1  var_2  var_3
# 0     A    1.0   True
# 1     B    2.0  False
# 2     D    NaN   True
```
* The right join will necessarily include all the columns and values from table_2
* Where matching variable (var_1) is not matched in table_1, there for these variables NaN will appear
* Right join will become a Left join if you swap the order of tables in the pd.merge() method


**14. Data Manipulation: Full (Outer) join**

```python
print(pd.merge(df_1, df_2, how = "outer"))
#   var_1  var_2  var_3
# 0     A    1.0   True
# 1     B    2.0  False
# 2     C    3.0    NaN
# 3     D    NaN   True
```
* In the outer join the output table will contain all the columns from both tables
* If for a given case/matching variable (var_1 here) there is no variable or match then NaN will apear


## 🚧 Warnings / Common Errors / Known Issues

⚠️ **The "column" argument in pd.DataFrame() method is not for renaming columns**

It is used to select which columns from the underlying data to include in the newly created DataFrame.

```python
my_df_columns = pd.DataFrame({"a": [1, 2], "b": [3, 4], "c":[5, 6]}, columns = ["a", "b"])
```

To rename columns in a DataFrame use pd.rename() method or columns() attribute:

```python
# Using the pd.rename() method
my_df_columns.rename(columns = {'a':'new_a', 'b':'new_b'}, inplace = True)

# Using the columns() attribute
my_df_columns.columns = ["newest_a", "newest_b"]

```

⚠️ **The "names" argument in pd.read_csv() method is not for renaming columns**

It is used to select which columns from the underlying file to load to the newly created DataFrame.

```python
my_csv = pd.read_csv("my_file.csv", names = ["A", "B"])
# If the file contains columns "A", "B" and "C", then the above line will skip column "C"
```

⚠️ **When indexing a range, the end index is not included**

If my_series_list_custom is the following Series:

a    100
b      2
c      3

Then in order to select the first two values (100 and 2) one should write:

```python
z = my_series_list_custom[0:2] # 0, 1, 2
```

As opposed to:

```python
z = my_series_list_custom[0:1] # 0, 1
```

This is because the end index is not included.

⚠️ **loc is an attribute not a methods so use square brackets [] not round brackets ()**

Since loc is an attribute one uses square brackets to access rows of a DataFrame in the fashion below:

```python
row_zero = test_df.loc[0]
test_df.loc[1] = 200
```

⚠️ **concat() is not a method or attribute of DataFrame object but belongs to pd instead**

You cannot add a new row to a data frame by writing:
```python
new_df = old_df.concat(new_row)
```
You'll get an error saying that the concat() is not DataFrame's attribute

Instead you use concat() from pd:
```python
new_df = pd.concat([old_df, new_df])
```

⚠️ **while melt() is a method of pd, it's opposite pivot() is a method of DataFrame**

To change from wide to narrow format refer to pd's method melt():
```python
pd.melt(df_wide, id_vars = "Person")
```
When performing the opposite operation, that is when going from narrow to wide refer to DataFrame's method pivot():
```pivot
df_narrow.pivot(index = ["Person"], columns = ["Variable"], values = ["Value"])
```


## 💡 Tips
💭 **Tip 1**

Description of tip 1.

💭 **Tip 2**

Description of tip 1.


## 📧 Contact
[![](https://img.shields.io/twitter/url?label=/SzymkowskiDev&style=social&url=https%3A%2F%2Ftwitter.com%2FSzymkowskiDev)](https://twitter.com/SzymkowskiDev) [![](https://img.shields.io/twitter/url?label=/kamil-szymkowski/&logo=linkedin&logoColor=%230077B5&style=social&url=https%3A%2F%2Fwww.linkedin.com%2Fin%2Fkamil-szymkowski%2F)](https://www.linkedin.com/in/kamil-szymkowski/) [![](https://img.shields.io/twitter/url?label=@szymkowskidev&logo=medium&logoColor=%23292929&style=social&url=https%3A%2F%2Fmedium.com%2F%40szymkowskidev)](https://medium.com/@szymkowskidev) [![](https://img.shields.io/twitter/url?label=/SzymkowskiDev&logo=github&logoColor=%23292929&style=social&url=https%3A%2F%2Fgithub.com%2FSzymkowskiDev)](https://github.com/SzymkowskiDev)

## 📄 License
[MIT License](https://choosealicense.com/licenses/mit/) ©️ 2019-2020 [Kamil Szymkowski](https://github.com/SzymkowskiDev "Get in touch!")

[![](https://img.shields.io/badge/license-MIT-green?style=plastic)](https://choosealicense.com/licenses/mit/)





