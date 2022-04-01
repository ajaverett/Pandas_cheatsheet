
# Pandas Cheatsheet

---

### Table of Contents
- [Importing Data](#importing-data)
    + [Pandas functions to import  data](#pandas-functions-to-import--data)
- [Inspect Data](#inspect-data)
    + [Pandas functions to inspect data](#pandas-functions-to-inspect-data)
- [Select Data](#select-data)
    + [Pandas functions to select data](#pandas-functions-to-select-data)
    + [Pandas functions to locate data with loc[] and iloc[]](#pandas-functions-to-locate-data-with-loc---and-iloc--)
- [Cleaning Data](#cleaning-data)
    + [Pandas functions to clean columns](#pandas-functions-to-clean-columns)
    + [Pandas functions to clean NaN values](#pandas-functions-to-clean-nan-values)
    + [Group By](#group-by)

---

# Importing Data 
### Pandas functions to import  data
<br>

__Read CSV file__ `df = pd.read_csv('data.csv')`

* Assigns data.csv to a dataframe called 'df'.



_Additional Arguments_

>>__Specify header__
>>
>>* The code below will assume the csv file has no column names (only data) thus _'df'_ column names will be numbers
>>`df = pd.read_csv('data.csv', header=None)`
>><br>
>>
>>* The code below will assume the first two lines in the CSV file are headers.
>>`df = pd.read_csv('data.csv', header=[0,1])`
>>
>>__Skip rows__
>>* The code below will ignore the first two rows in the CSV >>file.
>>`pd.read_csv('data.csv', skiprows=2, header=None)`
>>
>>__Encoding__
>>* The code below will read the csv file in the [encoding]>>(https://docs.python.org/3/library/codecs.html#standard-encodings) specified.
>>`pd.read_csv('data.csv', encoding ='utf-8')`
>>
>>__Encoding Errors__
>>* The code below will ignore any special characters it doesn't recognize. 
>>`pd.read_csv('data.csv', encoding_errors ='ignore')`


---

# Inspect Data

### Pandas functions to inspect data
<br>

__Columns__ `df.columns`

* Displays the column labels of the DataFrame.

__Shape__ `df.shape`

* Displays the length and width of the DataFrame.

__Heads and Tails__ `df.head(n)` `df.tails(n)`
* Displays the first _n_ rows of df
* Displays the last _n_ rows of df


__Describe__ `df.describe()`

* Gives the count, mean, std, min, 25%, 50%, 75%, and max of each column in _df_

__Value Counts__ `df['column_one'].value_counts()`
* Gives the count of each unique value in _column_one_.

_Additional Arguments_
>>
>>__Ascending__
>>* The code below will give the number of unique values in ascending order.
>>`df['column_one'].value_counts(ascending=True)`
>>
>>__Normalize__
>>
>>* The code below will give the number of unique values in percentages rather than raw count.
>>`df['column_one'].value_counts(normalize=True)`
<br>

__Continuous Data__

* The code below will give value counts for continuous data. Below, n is for how many bins pandas will auto-generate.
`df['column_one'].value_counts(bin = n)`

__Counting NaNs__

* The code below will include NaNs in the number of unique values returned.
`df['your_column'].value_counts(dropna=False)`

More tricks [here](https://re-thought.com/pandas-value_counts/)
</details>

---

# Select Data


### Pandas functions to select data 

<br>

__Show dataframe__ `df`

*  Displays the entire DataFrame.

__Show column(s)__ `df['column_one']`

* Displays the _column_one_ from _df_.

_Additional Arguments_
>>__Multiple columns__
>>* The code below will display both _column_one_ and _column_two_.
>>`df[['column_one','column_two']]`
>>
<br>

### Pandas functions to locate data with loc[] and iloc[]

<br>

The _loc[ ]_ command takes two arguments: one specifying the rows, and one specifying the columns. These arguments are separated by a comma. Finally, if ":" is passed alone as an argument, this will return all the data.

__Locating data with loc[]__:
*  `df.loc[:,:]` will return all the rows and columns 

* `df.loc[1,:]` will return row 1 with all the columns
* `df.loc[[1,6],:]` will return row 1 and 6 with all the columns
* `df.loc[[1:6],:]` will return row 1 through 6 with all the columns

* `df.loc[:,['column_one']]` will return all values under column_one
* `df.loc[:,['column_one','column_three']]` will return all values under column_one and column_three
* `df.loc[:,'column_one':'column_three']` will return all values under column_one through column_three

<br>

___Note 1:__ The above code assumes that the row index names are numbers. If the index row names were letters, `df.loc['A',:]` would display row _A_._



___Note 2:__ loc[] can be used with just one argument. Pandas assumes you are only sifting through rows and will by default display all column values respective to the rows._

<br>


__Filtering data with loc[]__
* `df.loc[df['gender']=='Male']` will return all data where gender is male
* `df.loc[df['race'].isin(['Black','Asian'])]` will return all data where race is either Black or Asian.
* `df.loc[(df['race'] != "White") & (df['sex'] == "Female")]` will return all Females who are not White.
* `df.loc[df['gender'].notnull() == True]` Since there may be null values in some columns, the code here will return all data where gender is known (not a null value).



<summary> Pandas functions to locate data with iloc[ ] </summary>

<br>

The _iloc[ ]_ command takes two arguments: one specifying the rows, and one specifying the columns. These arguments are separated by a comma. Finally, if ":" is passed alone as an argument, this will return all the data.

__Locating data with iloc[]__:
* `df.iloc[:,:]` will return all the rows and columns 

* `df.iloc[1,:]` will return row 1 with all the columns
* `df.iloc[[1,6],:]` will return row 1 and 6 with all the columns
* `df.iloc[[1:6],:]` will return row 1 through 6 with all the columns

* `df.iloc[:,1]` will return all values under the first column (0 would be the index)
* `df.iloc[:,[1,3]]` will return all values for column 1 and 3
* `df.iloc[:,1:3]` will return all values under column 1 through 3

<br>

___Note 1:__ The above code will only take integers since iloc is an index based function._

___Note 2:__ loc[] can be used with just one argument. Pandas assumes you are only sifting through rows and will by default display all column values respective to the rows._

<br>

---

# Cleaning Data


### Pandas functions to clean columns 

<br>

__Set index to a column__ `df.set_index('column_one')`
* Sets index to _column_one_.

__Rename Column(s)__ `df.rename(columns={"column_one": "col1"})`
* Renames _column_one_ to _col1_.

__Drop Column(s)__ `df.drop(columns=['B', 'C'])`
* Drops the respective column(s)

__Change Column(s) Datatype__ `df.astype({"Race":'category', "Age":'int64'})`
* Changes the _Race_ column to a categorical data type, changes _Age_ column to an integer data type.

___Note:__ In order to format these functions to multiple columns at once, the dictionary method as seen in the code below is an elegant way of performing this._
```
    dat.rename(columns = {
        'column_one':'col1',
        'column_two':'col2',
        'column_three':'col3
        })
```

### Pandas functions to clean NaN values 

__Drop NA__ `df.dropna()`
* drops all rows that contain null values


_Additional Arguments_
>>* `df.dropna(axis=1)` drops all columns that contain null values
>>* `df.dropna(thresh=n)` drops all rows have have less than n non null values
>>
<br>

__Fill NA__ `df.fillna(x)`
* Replace all null values with x

_Additional Arguments_
>>
>>* `df['Country'].fillna(method = ffill)` fills NA value with the value above the NA value.
>>
>>* `df['Country'].fillna(method = bfill)` fills NA value with the value below the NA value.
>>
>>* `df['Income'].fillna(df['Income'].mean())` drops all rows have have less than n non null values
>>
<br>

### Group By

Assume the columns: Gender, Num_Gadgets_made, Income

__Group By with Sum__ `df.groupby('Gender').sum()`
This code will group _df_ by gender using the sum of the column data. This may be useful to compare the raw total of Num_Gadgets_made by gender.


__Group By with Count__ `df.groupby('Gender').count()`
This code will group _df_ by gender using the count of the column data. This may be useful for seeing the total number of people by gender.

__Group By with Mean__ `df.groupby('Gender').mean()`
This code will group _df_ by gender using the mean of the column data. This may be useful to compare the average Income by gender.

---


