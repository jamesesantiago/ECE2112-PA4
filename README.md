# ECE2112-PA4

**By James Eon M. Santiago 2ECE-B**

This Repository Contains the Programming Assignment #4 for the Course "Advanced Computer Programming and Algorithms", which includes three python problems related to Module 4 - Data Wrangling and Visualization.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Before we start, we must first add `import pandas as pd, import matplotlib.pyplot as plt`, we also need a `pd.read_csv()` function to read the given data sheet.

```python
df = pd.read_csv('board2.csv')
df
```

A requirement of the column named "Average" is required to solve the python problems provided. We filter the subjects out using ``subjects = ['Math','Electronics','GEAS','Communication']`` and saving a new dataframe called "Average", by using the function `.mean()` to the given subjects and setting its axis to 1 to sort it by row.

```python
subjects = ['Math','Electronics','GEAS','Communication']
df['Average'] = df[subjects].mean(axis=1)
df['Average']
```

We must then concatenate this new DataFrame to the Original DataFrame by using `pd.concat()` function, with its axis set to 1 and save it.

```python
df = pd.concat([df],axis=1)
df
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# **(A) Visayas Communication Dataframe**

Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order: Name, Gender, Math, Electronics, Average. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Boolean Indexing is used to sort out the required conditions. For this, we only use the `.loc()` function.

We create a new DataFrame for this problem, in this case we will name our DataFrame `Adf`. With the function `.loc()` and parameters `(df['Track'] == 'Communication')&(df['Hometown'] == 'Visayas')`. We do this to not overwrite the original DataFrame that we made from the start.

```python
Adf = df.loc[(df['Track'] == 'Communication')&(df['Hometown'] == 'Visayas')]
```

We then create the DataFrame named VisComm using the `.loc()` function again with the parameters `:,['Name','Gender','Math','Electronics','Average']`

```python
VisComm = Adf.loc[:,['Name','Gender','Math','Electronics','Average']]
VisComm
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# **(B) Visayas Female Dataframe**

Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only: Name, Track, GEAS, Electronics, Average. Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not
overwrite VisFemale when performing this second filter.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Boolean Indexing is also used to sort out the required conditions. For this, we only use the `.loc()` function.

We create a new DataFrame for this problem, in this case we will name our DataFrame `Bdf`. With the function `.loc()` and parameters `(df['Average']>60)&(df['Track'] == 'Communication')&(df['Gender'] == 'Female')&(df['Hometown'] == 'Visayas')`. We do this to not overwrite the original DataFrame that we made from the start.


```python
Bdf = df.loc[(df['Average']>60)&(df['Track'] == 'Communication')&(df['Gender'] == 'Female')&(df['Hometown'] == 'Visayas')]
```

We then create the DataFrame named VisFemale using the `.loc()` function with the parameters `:,['Name','Track','GEAS','Electronics','Average']`

```python
VisFemale = Bdf.loc[:,['Name','Track','GEAS','Electronics','Average']]
VisFemale
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# **(C) Category Average Visualization**

Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown. For each feature, compute the mean of Average for every category using Pandas. Display the three summary tables. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature. Interpretation rule: Describe the observed dataset only. A difference in group means does not, by itself, establish that a feature causes a higher board-exam score.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

To start, we need to use the `.groupby()` function to group all data sheets with the same given parameters and add their values. And get their mean using the `.mean()` function.

```python
Track_Average = df.groupby('Track')['Average'].mean()
Track_Average

Gender_Average = df.groupby('Gender')['Average'].mean()
Gender_Average

Hometown_Average = df.groupby('Hometown')['Average'].mean()
Hometown_Average
```

`fig` is used to create the figure while `axes` assign an array for the individual subplots.

The `plt.subplots()` function is used to create a figure, the `1,3` values is read as a 1x3 grid of empty axes, and the `figsize` function is used to set the dimensions of the figure.

The `.plot()` function is used to set what kind of chart is used, while the `ax=axes[]` is used to target which subplot is going to be used, from the `1,3` values we set earlier. 

`plt_tightlayout()` allows the charts to be resized and to be made fit in the provided `figsize` values. While the `plt.show()` allows you to show the different charts.

The `print()` function is only used to make statements in the provided dataset.

```python
fig, axes = plt.subplots(1, 3, figsize=(10, 5))

Track_Average.plot(kind='bar', ax=axes[0])
Gender_Average.plot(kind='bar', ax=axes[1])
Hometown_Average.plot(kind='bar', ax=axes[2])
plt.tight_layout()
plt.show()

print ("For Track Averages, the Communication track achieved the highest sample mean.\nFor Gender, Males achieved the highest sample mean.\nFor Hometown, Luzon has achieved the highest sample mean.")
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# **Thank you for reading!!!**
