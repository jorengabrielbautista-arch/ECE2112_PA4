### Joren Gabriel P. Bautista
### 2ECE-D

# ECE2112_PA4
#     DATA WRANGLING AND DATA VISUALIZATION
## Purpose
  This README explains the various functions of the different lines of code that was used in this project.  
  ## A.VISAYAS COMMUNICATION DATAFRAME
### Instruction/Requirements

* Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. 
* Retain only these columns, in the stated order:
**Name, Gender, Math, Electronics, Average**

* Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

### Full Code

```python
import pandas as pd
board2 = pd.read_excel("board2.xlsx")

  board2['Average'] = board2[['Math','Electronics', 'GEAS','Communication']].mean(axis=1)

      VisComm = board2.loc[(board2['Hometown']== 'Visayas') & 
                       (board2['Track']== 'Communication'),
                        ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
```
#### Code Breakdown
```python
import pandas as pd
board2 = pd.read_excel("board2.xlsx")
```
> **Explanation:**
> Import `import pandas as pd data` manipulation library and assigns it to *pd* <br>
> While `board2 = pd.read_excel("board2.xlsx")`, reads the excel file and assisngs its value to *board2*

```python
board2['Average'] = board2[['Math','Electronics', 'GEAS','Communication']].mean(axis=1)

```
> **Explanation:** <br>
> This line of code is responsible for making a new column named 'Average' in the dataset *board2* <br>
> While the `board2[['Math','Electronics', 'GEAS','Communication']].mean(axis=1)`, selects the named columns to get the average of.

```python
        VisComm = board2.loc[(board2['Hometown']== 'Visayas') &
           (board2['Track']== 'Communication'),
              ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
```
> **Explanation:** <br>
> This creates a new data frame named *VisComm*, which is then assigned with values from board2. <br>
> This part of the code `board2.loc[(board2['Hometown']== 'Visayas') & (board2['Track']== 'Communication')`, selects the data, where both the conditions are true, which are their hometown is *Visayas* and that their track is *Communication* <br>
> Lastly this part: `['Name', 'Gender', 'Math', 'Electronics', 'Average']` , is responsible for selecting the columns that would be included.

## B. VISAYAS FEMALE DATAFRAME
### Instruction/Requirements
* Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. <br>
* Retain only: **Name, Track, GEAS, Electronics, Average**
* Display VisFemale.
* Then display only the rows of VisFemale whose Average is at least 60. Do not
overwrite VisFemale when performing this second filter.

### Full Code

```python
 VisFemale = board2.loc[
                (board2['Hometown']== 'Visayas') & 
                 (board2['Gender']== 'Female'),
                  ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
  VisFemale
  
      VisFemale.loc[VisFemale['Average']>60]
```

#### Code Breakdown
```python
     VisFemale = board2.loc[
                (board2['Hometown']== 'Visayas') & 
                 (board2['Gender']== 'Female'),
                  ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
```
> **Explanation:** <br>
> This creates a new data frame named *VisFemale*, which is then assigned with values from board2. <br>
> This part of the code `board2.loc[(board2['Hometown']== 'Visayas') & (board2['Gender']== 'Female')`, selects the data, where both the conditions are true, which are their hometown is *Visayas* and that their gender is *Female* <br>
> Lastly this part: `['Name', 'Track', 'GEAS', 'Electronics', 'Average']` , is responsible for selecting the columns that would be included.


```python
     VisFemale
```
> **Explanation:** <br>
> This displays the table, showing *Name, Track, GEAS, Electronics and Average* of all the data that met the two required conditions.


```python
      VisFemale.loc[VisFemale['Average']>60]
```
**Explanation:** <br>
> This filters out all the other data that doesn't meet the requirements of having an average greater than 60, while simultaneously not changing the data store in *VisFemale*

## C. CATEGORY-AVERAGE VISUALIZATIO
### Instruction/Requirements
* Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown. <br>
***a. For each feature, compute the mean of Average for every category using Pandas.*** <br>
***b. Display the three summary tables.*** <br>
***c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.*** <br>
***d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.*** <br>
### Full Code

```python
import matplotlib.pyplot as plt

mbt= board2.groupby('Track')['Average'].mean().reset_index()
mbg = board2.groupby('Gender')['Average'].mean().reset_index()
mbh= board2.groupby('Hometown')['Average'].mean().reset_index()

print("Mean By Track:\n")
mbt

print("Mean By Gender:\n")
mbg

print("Mean By Hometown:\n")
mbh

fig, axes = plt.subplots(1,3, figsize = (17,5))

axes[0].bar(mbt['Track'], mbt['Average'], color = 'Cyan')
axes[0].set_title('Track Average')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Average')

axes[1].bar(mbg['Gender'], mbg['Average'], color = 'Teal')
axes[1].set_title('Gender Average')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Average')


axes[2].bar(mbh['Hometown'], mbh['Average'], color = 'Pink')
axes[2].set_title('Hometown Average')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Average')

text = ('Feature 1: Communication recorded the highest average with a score of *67.975*'
'\nFeature 2: Male recorded the highest average with a score of *67.18333*'
'\nFeature 3: Visayas recorded the highest average with a score of *6.08333*'
)

fig.text(0.15, -0.15, text)

```

#### Code Breakdown
```python
import matplotlib.pyplot as plt
```
> **Explanation:** <br>
> This imports `import matplotlib.pyplot as plt` the matplot library and assign it to plt.

```python
mbt= board2.groupby('Track')['Average'].mean().reset_index()
mbg = board2.groupby('Gender')['Average'].mean().reset_index()
mbh= board2.groupby('Hometown')['Average'].mean().reset_index()
```
> **Explanation:** <br>
> * This `mbt= board2.groupby('Track')['Average']` groups Track and Average, and this `.mean().reset_index()` takes the average scores of each track and then resets the index <br>
> * This `mbg= board2.groupby('Gender')['Average']` groups Gender and Average, and this `.mean().reset_index()` takes the average scores of each gender and then resets the index <br>
> * This `mbh= board2.groupby('Hometown')['Average']` groups Howmetown and Average, and this `.mean().reset_index()` takes the average scores of each track and then resets the index <br>

```python
print("Mean By Track:\n")
mbt

print("Mean By Gender:\n")
mbg

print("Mean By Hometown:\n")
mbh
```

> **Explanation:** <br>
> While this shows the averages in tabular form.


```python
fig, axes = plt.subplots(1,3, figsize = (17,5))
```

> **Explanation:** <br>
> This generate a single figure window containing a row of three side-by-side subplots. `(1,3, figsize = (17,5))` Is responsible for generating one row of subplot and 3 columns of subplot. While `figsize = (17,5)` is for setting the dimensions of the window.

```python

axes[0].bar(mbt['Track'], mbt['Average'], color = 'Cyan')
axes[0].set_title('Track Average')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Average')
```
> **Explanation:** <br>
> * `axes[0]` Targets the first subplot in the window, `.bar()` is a function that draws a vertical bar chart for the data. While `mbt['Track'], mbt['Average']` sets the x-axis and y-axis data respectively, both taking from the data frame named *mbt*.
> * `.set_title('Track Average')` This function names the subplot as *Track Average*
> * `.set_xlabel('Track')` & `axes[0].set_ylabel('Average')` labels the x-axis and y-axis respectively as *Track* and *Average*.

```python
axes[1].bar(mbg['Gender'], mbg['Average'], color = 'Teal')
axes[1].set_title('Gender Average')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Average')


axes[2].bar(mbh['Hometown'], mbh['Average'], color = 'Pink')
axes[2].set_title('Hometown Average')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Average')
```
> **Explanation:** <br>
> * This is mostly similar to the code for `axes[0]`, it's just that this time we are editing the 2nd and 3rd subplot, so we'd be using `axes[1]` and `axes[2]`.
> * Other changes are instead of taking data from the data frame, *mbt*`(mean by track)`, subplot 2 would be taking from data frame *mbg*`(mean by gender)` and the 3 subplot would be taking data from *mbh* `(mean by hometown)`.
> * The x-axis will instead take data from *Gender*`mbg['Gender']` for the 2nd subplot and *Hometown*`mbh['Hometown']` for the 3rd subplot
> * The subplot would be named Gender Average and Hometown Average for the 2nd and 3rd subplot, this is due to the code `axes[1].set_title('Gender Average')` and `axes[2].set_title('Hometown Average')`
> * Of course the labels for the x-axis would be changed for their corresponding subplot, `axes[1].set_xlabel('Gender')`  and `axes[2].set_xlabel('Hometown')`.


 ```python
text = ('Feature 1: Communication recorded the highest average with a score of *67.975*'
'\nFeature 2: Male recorded the highest average with a score of *67.18333*'
'\nFeature 3: Visayas recorded the highest average with a score of *6.08333*'
)

fig.text(0.15, -0.15, text)
 ```
 **Explanation:** <br>
> This three are the written statements identifying the category with the highest sample
mean for each feature.
> `fig.text(0.15, -0.15, text)` places the content of `*text* ` at position *0.15, -0.15*
