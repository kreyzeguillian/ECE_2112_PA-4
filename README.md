# PA-4 Documentation  
Before anything else, the `board2.xlsx` file that contains the data frame is downloaded from the course site  

<img src="https://github.com/kreyzeguillian/Programming-Assigments/blob/main/PA-4/ss4githubPA4.2.png" alt="Alt text" width="600"/>

After downloading, the excel file is placed within the same directory as the jupyter notebook  

<img src="https://github.com/kreyzeguillian/Programming-Assigments/blob/main/PA-4/ss4githubPA4.png" alt="Alt text" width="500"/>

---
### ECE BOARD EXAM PROBLEM:
Using data wrangling and data visualization technique with storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.

#### DATA WRANGLING

&nbsp;&nbsp;&nbsp;&nbsp;1. Create the following data frames based on the format provided:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Output:

| Name   | Gender |   Track |   Math |
|---:|:------------------|------:|------:|
| S4 | Male | Instrumentation | 65 |
| S11 | Female | Communication | 48 |
| S22 | Female | Communication | 64 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b. Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female

### **Code/Explanations**:  

**Cell 1**:
```
# Imports the pandas and matplotlib libraries
import pandas as pd
import matplotlib.pyplot as plt
```
- The pandas library is imported as `pd` while the matplotlib library is imported as `plt`.

**Cell 2**:
```
# Loads and displays the excel file
df = pd.read_excel('board2.xlsx')
df
```
- The `board2.xlsx` file is loaded using the `pd.read_excel()` function, and then displayed.

**Output of Cell 2**:

|    | Name   | Gender   | Track            | Hometown   |   Math |   Electronics |   GEAS |   Communication |
|---:|:-------|:---------|:-----------------|:-----------|-------:|--------------:|-------:|----------------:|
|  0 | S1     | Male     | Instrumentation  | Luzon      |     58 |            89 |     75 |              78 |
|  1 | S2     | Female   | Communication    | Mindanao   |     52 |            75 |     90 |              52 |
|  2 | S3     | Female   | Instrumentation  | Mindanao   |     83 |            74 |     77 |              57 |
|  3 | S4     | Male     | Instrumentation  | Visayas    |     65 |            58 |     91 |              68 |
|  4 | S5     | Male     | Communication    | Luzon      |     59 |            86 |     43 |              88 |
... | ... | ... | ... | ... | ... | ... | ... | ... |
| 25 | S26    | Female   | Instrumentation  | Visayas    |     71 |            47 |     83 |              62 |
| 26 | S27    | Male     | Microelectronics | Visayas    |     70 |            47 |     40 |              86 |
| 27 | S28    | Male     | Communication    | Visayas    |     85 |            53 |     80 |              53 |
| 28 | S29    | Male     | Instrumentation  | Mindanao   |     73 |            48 |     71 |              62 |
| 29 | S30    | Male     | Instrumentation  | Luzon      |     78 |            81 |     57 |              56 |

**Cell 3**:
```
# Creates/displays a subset of the DataFrame 'df' to contain specific data
Instru = df.loc[(df['Track'] == 'Instrumentation') &
                (df['Hometown'] == 'Luzon') &
                (df['Electronics'] > 70),
                ['Name', 'GEAS', 'Electronics']].reset_index(drop=1)
Instru
```
- The data frame `df` is indexed to create a new subset.

**Output of Cell 3**:  

|    | Name   |   GEAS |   Electronics |
|---:|:-------|-------:|--------------:|
|  0 | S1     |     75 |            89 |
|  1 | S8     |     64 |            81 |
|  2 | S30    |     57 |            81 |

**Cell 4**:
```
# Adds an additional column named 'Average' where the mean of the grades is obtained
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

# Creates a subset of the DataFrame 'df' to contain specific data
Mindy = df.loc[(df['Hometown'] == 'Mindanao') &
               (df['Gender'] == 'Female') &
               (df['Average'] >= 55), 
               ['Name', 'Track', 'Electronics', 'Average']].reset_index(drop=1)
Mindy
```
- A column named `Average` is added and contains the average of the grades.
- The data frame `df` is indexed to create a new subset.

**Output of Cell 4**:

|    | Name   | Track            |   Electronics |   Average |
|---:|:-------|:-----------------|--------------:|----------:|
|  0 | S2     | Communication    |            75 |     67.25 |
|  1 | S3     | Instrumentation  |            74 |     72.75 |
|  2 | S15    | Microelectronics |            41 |     59    |
|  3 | S17    | Microelectronics |            79 |     70.5  |
|  4 | S20    | Communication    |            60 |     66.5  |
---

#### DATA VISUALIZATION

&nbsp;&nbsp;&nbsp;&nbsp;2. Create a visualization that shows how the different features contributes to average grade. Does chosen track in college, gender, or hometown contributes to a higher average score?

### **Code/Explanations**:  

**Cell 1**:
```
# Creates a plotter function to avoid repetition
def plotter(column):
    # Sets the figure's size to 5x6
    plt.figure(figsize=(5,6))
    
    # Creates a bar graph with df[column] in the x-axis and df['Average'] in the y-axis
    plt.bar(df[column], df['Average'])
    
    # Labels the graph
    plt.title('Average Grades by ' + column)

    # Labels the plot's y-axis
    plt.ylabel('Average Grade')

    # Displays the plot
    plt.show()

# Function call to create a plot by 'Gender'
plotter('Gender')

# Function call to create a plot by 'Track'
plotter('Track')

# Function call to create a plot by 'Hometown'
plotter('Hometown')
```
- Three plots are created to visualize the features with respect to the average grades.

**Output of Cell 1**:

<img src="https://github.com/kreyzeguillian/Programming-Assigments/blob/main/PA-4/ss4githubPA4.3.png" alt="Alt text" height="250"/><img src="https://github.com/kreyzeguillian/Programming-Assigments/blob/main/PA-4/ss4githubPA4.4.png" alt="Alt text" height="250"/><img src="https://github.com/kreyzeguillian/Programming-Assigments/blob/main/PA-4/ss4githubPA4.5.png" alt="Alt text" height="250"/>
