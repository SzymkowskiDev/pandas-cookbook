
# Pandas Cookbook
How to perform various data cleaning and manipulation tasks in Pandas.

## 🚀 How to run
Download and run Jupyter notebooks

## 🎓 Learning Materials
* w3schools Pandas tutorial [w3schools Pandas tutorial](https://www.w3schools.com/python/pandas/default.asp)
* javapoint Pandas tutorial [javapoint Pandas tutorial](https://www.javatpoint.com/python-pandas)
* geeksforgeeks Pandas tutorial [geeksforgeeks Pandas tutorial](https://www.geeksforgeeks.org/pandas-tutorial/?ref=lbp)
* kaggle Pandas tutorial [kaggle Pandas tutorial](https://www.kaggle.com/learn/pandas)
* Pandas documentation [Pandas documentation](https://pandas.pydata.org/getting_started.html)
* Pandas GitHub repository [Pandas GitHub repository](https://github.com/pandas-dev/pandas)

## 📋 Modules
```python
import pandas as pd
```

## 📝 Cookbook

Pandas offers 1-dimensional Series, 2-dimensional DataFrames and used to offer 3-dimensional Panels, that were deprected (since version 0.20.0) in favour of representing 3-D data with a MultiIndex on a DataFrame via the to_frame() method or with the xarray package. Here we deal briefly with Series and extensively with DataFrames.

**1. Creating data types: Series**

* Series is created with the pd.Series() method
* pd.Series() method takes list or dictionary as data argument
* Elements in a series are labelled
* By default labells are integers 0, 1, 2, ...
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

Description of the example.

```python
CODE GOES HERE
```


**Example 2. Title**

Description of the example.
```python
CODE GOES HERE
```

## ⚙ Configurations
Sth

## 💡 Tips
💭 **Tip 1**

Description of tip 1.

💭 **Tip 2**

Description of tip 1.

## 🚧 Warnings / Common Errors / Known Issues

⚠️ **Warning 1**

Description of warning 1.

⚠️ **Warning 2**

Description of warning 2.

## Contents
1. How to create data types
2. How to access elements in data types
3. How to modify data types

## 📧 Contact
[![](https://img.shields.io/twitter/url?label=/SzymkowskiDev&style=social&url=https%3A%2F%2Ftwitter.com%2FSzymkowskiDev)](https://twitter.com/SzymkowskiDev) [![](https://img.shields.io/twitter/url?label=/kamil-szymkowski/&logo=linkedin&logoColor=%230077B5&style=social&url=https%3A%2F%2Fwww.linkedin.com%2Fin%2Fkamil-szymkowski%2F)](https://www.linkedin.com/in/kamil-szymkowski/) [![](https://img.shields.io/twitter/url?label=@szymkowskidev&logo=medium&logoColor=%23292929&style=social&url=https%3A%2F%2Fmedium.com%2F%40szymkowskidev)](https://medium.com/@szymkowskidev) [![](https://img.shields.io/twitter/url?label=/SzymkowskiDev&logo=github&logoColor=%23292929&style=social&url=https%3A%2F%2Fgithub.com%2FSzymkowskiDev)](https://github.com/SzymkowskiDev)

## 📄 License
[MIT License](https://choosealicense.com/licenses/mit/) ©️ 2019-2020 [Kamil Szymkowski](https://github.com/SzymkowskiDev "Get in touch!")

[![](https://img.shields.io/badge/license-MIT-green?style=plastic)](https://choosealicense.com/licenses/mit/)





