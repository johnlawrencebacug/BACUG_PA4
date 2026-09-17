# PROGRAMMING ASSIGNMENT_4
### BACUG, John Lawrence B. | 2ECE-C
### Date submitted: 09/17/2026

## Objectives:
Use the same ECE Board Exam 2 dataset supplied for Experiment 4. Work in a Jupyter Notebook
using Pandas and a Python plotting library used in class. Use the dataset’s existing column labels,
including Name, Gender, Track, Hometown, Math, GEAS, Electronics, and Average.

 * Derive all tables and plot values from the dataset. Do not manually type rows, category means, or
plotted values.
* When applying more than one condition, make every condition explicit in the filtering expression.
* Keep the original DataFrame unchanged.
* Every graph must have a title, axis labels, readable category labels, and a consistent scale appro-
priate to the data.

## **A. VISAYAS COMMUNICATION DATAFRAME**
* `import` pandas as `pd` - Imports pandas library into the code and is given the name plt.  

* `df.describe()` - describes the imported xlsx file.

* `pd.read_excel` - Loads the imported xlsx file into the code.
  
* `VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')][['Name','Gender','Math','Electronics', 'Average']]` - Creates a data frame called `VisComm`, but filters are added specifically whose Hometown is Visayas and Track is Communication, displaying their Name, Gender, Math, Electronics, and calculated Average (mean of Math and Electronics).
  
* `df['Average'] = df[['Math', 'Electronics']].mean(axis=1)` - This line of code gets the mean of the columns inside the bracket, and the `(axis=1)` tells the code that the average is taken specifically from the row instead of the column.

```python
import pandas as pd

df = pd.read_excel('board2.xlsx')
df

df.describe()

df['Average'] = df[['Math', 'Electronics']].mean(axis=1)

VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')][['Name','Gender','Math','Electronics', 'Average']]
VisComm
```
## **B. VISAYAS FEMALE DATAFRAME**
* `df['Average'] = df[['GEAS','Electronics']].mean(axis=1)` - Gets the mean of the columns inside the brackets called `GEAS`, and `Electronics`. The `(axis=1)` tells the code that the average is taken specifically from the row instead of the column.

* `VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name','Track','GEAS','Electronics', 'Average']]` - Creates a data frame called `VisFemale` and calls the row that has the Hometown as Visayas, Gender is female, while also creating a filter that displays only Name, Track, GEAS, Electronics and the average for both.

* `display(VisFemale[VisFemale['Average'] >= 60])` - calls the VisFemale but only for those whose average is greater than or equal to 60.

```python
df['Average'] = df[['GEAS','Electronics']].mean(axis=1)

VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][['Name','Track','GEAS','Electronics', 'Average']]
VisFemale

display(VisFemale[VisFemale['Average'] >= 60])
```
## **C. CATEGORY-AVERAGE VISUALIZATION**
* `df.groupby()[[]]` - This code calls the columns that is needed to be separated and is inserted inside the parenthesis and the column name that needs to be calculated using `.mean()` is inside the double bracket.

* `.mean()` - This code is used to calculate the average of a certain column.

* `.reset_index()` - This code resets the index of the DataFrame to default integer index.

* `import matplotlib.pyplot as plt` - Imports matplotlib library into the code and is given the name plt.

* `plt.subplots(1, 3, figsize=(15, 5), sharey=True)` - This creates a 3 plot that is side by side and has 15in width and 5in length, whilst they are sharing the same y axis.

* `axes[].bar()` - This code creates a bar chart for the values that will be inputed.

* `axes[].set_title()` - This code creates a specific name for a specific bar in the bar chart.

* `axes[].set_ylabel()` - This code specifically names the y-axis of the bar chart.

* `plt.ylim()` - This code sets the y-axis' limit.

* `plt.tight_layout()` - This code is used to prevent overlaps, uneven spacing to the graphs, and improves the organization of the layout.

```python
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

Track = df.groupby('Track')[['Average']].mean().reset_index()
Track

Gender = df.groupby('Gender')[['Average']].mean().reset_index()
Gender

Hometown = df.groupby('Hometown')[['Average']].mean().reset_index()
Hometown

import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 3, figsize=(15, 5), sharey=True)

axes[0].bar(Track['Track'], Track['Average'])
axes[0].set_title('Mean Average by Track')
axes[0].set_ylabel('Mean Avreage')

axes[1].bar(Gender['Gender'], Gender['Average'], color='red')
axes[1].set_title('Mean Average by Gender')

axes[2].bar(Hometown['Hometown'], Hometown['Average'], color='yellow')
axes[2].set_title('Mean Average by Hometown')

plt.ylim(0, 100)
plt.tight_layout()
plt.show()


#### README file version update history
September 17, 2026 - README file uploaded.
