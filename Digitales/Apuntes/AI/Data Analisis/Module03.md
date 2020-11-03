# Module 03

## Descriptive Statistics

Descriptive statistical analysis helps to describe basic features of a dataset and obtains short summary about the sample and measures of the data.

The `describe()` method of pandas gives us an overview of the dataset. This will provide a clear idea of the distribution of the the different variables.

```python
df.describe()
```

The `value_counts()` method will count the amount of values given for a categorical variable (columns)

```python
drive_wheels_counts = df["drive-wheels"].value_counts()
```

| Drive-wheels | Count |
| ------------ | ----- |
| 2 frnt       | 321   |
| 2-bck        | 32    |
| 4-whe        | 45    |

## Grouping data

Grouping data in pandas is quite easy

```python
# First we select the columns we want to group
df_test = df[["col1","col2","col3"]]
# Then we group the data according to the columns we want
df_grp = df_test.groupby(["drive-wheels", "body-style"], as_index=False).mean()
```

A little tweak we can make to make this table more visually appealing is to use the `pivot()` mehtod

```python
df_pivot = df_grp.pivot(index='drive-wheels', columns="body-style")
```

*Hint: a heat map will go great with this kind of data*

## Correlation

Correlation is a statistical metric for measuring to what extent different variables are interdependent. Correlation provides information on how two variable change overtime and how changes in one affects the other. Scatter plots are great for visualizing this data.

To visualize a scatter plot in Python we'll make good use of the [Seaborn](https://seaborn.pydata.org/tutorial.html) library.

```python
import seaborn as sns
sns.regplot(x="engine-size", y="price", data=df)
plt.ylim(0,)
```

### Pearson correlation

On way to measure the strength of the correlation between continuous numerical variable is by using a method called Person correlation. Pearson correlation method will give you two values: the **correlation coefficient** and the **P-value.**

The **Correlation coefficient** can go from -1 to 1 and indicating a larga positive correlation if the value near to +1 and a large negative correlation is the value is near -1. if the value is close to 0, this means there's no correlation or that the correlation is weak.

The **P-Value** measures the certainty of the correlation.

* P-value < 0.001 **Strong** certainty in the result
* P-value < 0.05 **Moderate** certainty in the result
* P-value < 0.1 **Weak** certainty in the result
* P-value > 0.1 **No certainty** in the result

To calculate the Pearson correlation we can use the `stats` package from the `scipy` module.

```python
pearson_coef, p_value = stats.pearsonr(df["horsepower"], df["price"])
```



## Analysis of Variable

**ANOVA** can be used to find the correlation between different groups of a categorical variable. From an **ANOVA** analysis we obtain 2 values. 

*Better explained: https://www.youtube.com/watch?v=ITf4vHhyGpc*

* **F-Test score:** variation between sample group means divided by variation within sample group 

* **P-Value:** Confidence degree 
  $$
  F = \frac{\text{Variance between groups}}{\text{Variance within the group}}
  $$
  

$$
S^2  = \frac{\sum_{i=1}^n (x_i -\bar{x})}{n-1}
\\
S^2	=	sample variance\\
x_i	=	the value of the one observation\\
\bar{x}	=	the mean value of all observations\\
n	=	the number of observations
$$

