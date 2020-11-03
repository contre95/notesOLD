# Data Wrangling

## Data Pre-Processing

###  Dealing with missing data

There are many ways to deal with missing values and this is regardless of Python, R or whatever tool you use. Of course, each situation is different and should be judged differently. However, these are the typical options you can consider.

* Dropping missing values 
  * Dropping all data of that type (Dropping the column)
  * Dropping the data entry (Dropping the row)
* Replace the missing value
  * Replace it with an average ( of similar data-points ) (if numerical)
  * Replace by frequency (Same approach like average for non-numerical values)
  * Replace based on other functions (*Old cars tend to run on gasoline*)
  * Leave it as missing

Pandas provide some functions to help us deal with missing data.

To **drop missing** values from a dataframe we can use the dataframe method `dropna()`.

```python
# Assuming we have a Dataframe loaded in the variable df
df.dropna(
    subset=['column-with-missing-values'],
	axis=0, # 0 drops the entire row, 1 drop the column
    inplace=True # Perform the change within the same dataframe .If False a new dataframe is returned
)
# In case inplace=False
new_df = df.dropna( ... , inplace=False) # This doesn't perform any change on the df datafram.
```

*Source: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html*

To **replace missing** values we can use the method `replace()`. In the following example we would replace the missing values with the *mean* of that same column. 

```python
# Assuming we have a Dataframe loaded in the variable df
mean = df['column-with-missing-values'].mean()
missing_value_format = None # This cloud be 0 , None, NaN (np.nan) or whatever your missing values are filled with.
df['columns-with-missing-values'].replace(missing_value, mean) 
```

## Data Formatting

With pandas dataframe we can easily format an entire column with a single operation.

Imagine the case we have a temperature in Farenheits  and we need to format it to Celsius

```python
# Assuming we have a Dataframe loaded in the variable df
df['temperature-far'] = (df['temperature-far'] -32) *(5/9)
df.rename(columns=["temperature-fat","temperature-cel"], inplace=True)
```

We can do the same for any kind of operation o applying any kind of function. 

Changing types is also very useful. There's a method called `astype()` that can come very handy in these situations.

```python
# Assuming we have a Dataframe loaded in the variable df
df['price'] = df["price"].astype("int")
```

This will apply the Python's built in function `int()` to every single of the column "price"

## Data Normalization

In statistics and applications of statistics, normalization can have [a range of meanings](https://en.wikipedia.org/wiki/Normalization_(statistics)). In the simplest cases, normalization of ratings means adjusting values measured on different scales to a notionally common scale, often prior to averaging. (Not to be confused with Database normalization).

Sometime the nature of the data biases the linear regression model to weigh some values more than other. Like the **age** and **income** example.

| Age  | Income |
| :--- | ------ |
| 20   | 100000 |
| 30   | 20000  |
| 40   | 500000 |

To avoid this, we can normalize these two variables into values that range from zero to one. In this particular case, dividing income by the Max value (50000) 

| Age  | Income |
| :--- | ------ |
| 0.2  | 0.2    |
| 0.3  | 0.4    |
| 0.4  | 1      |



This will help these two variable to have similar influence to the model we'll build later.

### Methods of normalizing data

#### Simple feature scaling

$$
Xnew = \frac{Xold}{Xmax}
$$

```python
# With pandas
df["age"] = df["age"] /  df"age"].max()
```



#### Min-Max

$$
Xnew = \frac{Xold - Xmin}{Xmax-Xmin}
$$



```python
# With pandas
df["age"] = (df["age"]-df["age"].(min)) / (df["age"].max() - df["age"].min())
```



#### Z-Score

$$
Xnew = \frac{Xold- \mu}{\sigma} \\ 
\mu = \text{average of the feature} \\
\sigma =\text{standard deviation}
$$

```python
# With pandas
df["age"] = (df["age"] - df["age"].mean()) / df["age"].std()
```



## Data Binning

Binning is when you group values together into bins. For example, you can bin “age” into [0 to 5], [6 to 10], [11 to 15] and so on. Sometimes, binning can improve accuracy of the predictive models. In addition, sometimes we use data binning to group a set of numerical values into a smaller number of bins to have a better understanding of the data distribution.i

The functions **linespace** returns **numpy** array that comes very handy for pandas dataframe. the `linspace` function just divide several values in "categories". 

```python
bins = np.linspace(min(df['price']), max(df['price']), 4) # => These will divide is int 4 block which will let us define 3 categories (intervals) (bins) (groups)
group_names = ["Low", "Medium", "High"]

df["new-price-categorization"] = pd.cut(df["price"],bins,labels=group_names,include_lowest=True)

```

the `pd.cut()` method will segment and sort the data values into these new categories (bins)

## Categorical Variables into Quantitative 

The opposite of Data Binning would be making these categorical variables into qualitative ones. We do this by adding a new column with the name of the category and filling the cells with 0 or 1 depending if that row corresponds to that category.

We can get that dataframe easily with pandas `get_dummies()` method. This method is often call "One-hot encoding"

```python
pf.get_dummies(df['fuel'])
```

This will return the next dataframe

| Oil  | Gas  |
| ---- | ---- |
| 0    | 1    |
| 1    | 0    |
| 1    | 0    |

