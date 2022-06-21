
# Pandas Cookbook
How to perform various data cleaning and manipulation tasks in Pandas.

## Contents
1. How to run
2. Learning Materials
3. Modules
4. Configurations
5. Cookbook
  5.1. Creating data types: Series
  5.2. Creating data types: DataFrame
  5.3. Loading files into a DataFrame: CSV
  5.4. Loading files into a DataFrame: JSON
6. Warnings / Common Errors / Known Issues
7. Tips
8. Contact
9. License

## 🚀 How to run
Download and run Jupyter notebooks

## 🎓 Learning Materials
* [w3schools Pandas tutorial](https://www.w3schools.com/python/pandas/default.asp)
* [javapoint Pandas tutorial](https://www.javatpoint.com/python-pandas)
* [geeksforgeeks Pandas tutorial](https://www.geeksforgeeks.org/pandas-tutorial/?ref=lbp)
* [kaggle Pandas tutorial](https://www.kaggle.com/learn/pandas)
* [Pandas documentation](https://pandas.pydata.org/getting_started.html)
* [Pandas GitHub repository](https://github.com/pandas-dev/pandas)

## 📋 Modules
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





