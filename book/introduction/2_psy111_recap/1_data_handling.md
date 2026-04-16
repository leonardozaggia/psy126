---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# 2.1 Data Handling 
First, we load the [dataset](https://github.com/leonardozaggia/psy126/tree/main/book/introduction/2_psy111_recap/data):

## Loading Data

```{code-cell}
import pandas as pd

df_c = pd.read_csv("./data/child_num_skills.csv", index_col=0)  
df_c.head()  
```

## Exploring Data
Once loaded, we can inspect the structure of our dataset using a variety of methods.
We can use .info() to get a closer look into our data:

```{code-cell}
print(df_c.info())        # Summary including data types and non-null counts
print(df_c.columns)       # List of column names
```

## Handling Missing Data
Real-world datasets often include missing values. **Child Numeracy Skills** does not contain any missing data, so let us load the **Yeatman** dataset for this part:

```{code-cell}
df_y = pd.read_csv("https://yeatmanlab.github.io/AFQBrowser-demo/data/subjects.csv",
                      usecols=[1,2,3,4,5,6,7],
                      na_values="NaN",
                      index_col=0)
print(df_y.head())
```

We can count the number of missing value per category:

```{code-cell}
missing_values_count = df_y.isna().sum()    # Count of missing values per column

print("In our dataset the following columns have the specified number of missing values:")
print(missing_values_count)
```
`NaN` values need to be removed, or we won't be able to perform our analyses. We could fix our dataset using either one of the following strategies:
- Use `pandas` method `.dropna()`.
- Use `pandas` method `.fillna()`.

```{code-cell}
df_y['Handedness'] = df_y['Handedness'].fillna(0)     # Replace missing values in a column
df_y = df_y.dropna()                                  # Drop all rows with any missing value

df_y.head()
```

## Filtering and Subsetting
Subset data through *logical indexing* or by selecting specific columns: 

```{code-cell}
df_c_filtered = df_c[df_c["time"] > 40]         # Rows where total time taken is greater than 40
df_c_subset = df_c[["time", "addit2"]]          # Only keep selected columns

df_c_filtered.head()                             
```
Alternatively we can drop specific columns using the [`.drop()`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html) method.
```{code-cell}
df_only_items = df_c.drop(columns=['class', 'time'])

df_only_items.head()                        
```

```{admonition} Full control
:class: tip

Here we only saw few application. If you want to feel like you are in **full control**, I higly recommend checking `pandas` [documentation](https://pandas.pydata.org/docs/getting_started/index.html).

```
