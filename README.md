## EXPERIMENT 4:DATA WRANGLING AND DATA VISUALIZATION

### Instructions:
Download the ECE Board Exam 2 dataset found on this link: bit.ly/ECEBoardExamDataset and write a Python script/code in the Jupyter Notebook to do the given problems. You may submit your Jupyter notebook in the dedicated submission bin.

ECE BOARD EXAM PROBLEM: Using data wrangling and data visualization technique with storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.

1. Create the following data frames based on the format provided:

a. Filename: Instru = ["Name", "GEAS", "Electronics >70"]; where track is constant as Instrumentation and hometown Luzon

b. Filename: Mindy = ["Name", "Track", "Electronics", "Average >= 55"]; where hometown is constant as Mindanao and gender Female

Code: 
```python
# Start
import pandas as pd # Import the pandas library

df = pd.read_csv('board2.csv') # Read the 'board2.csv' file and load it
df

# a. Filename: Instru = ["Name", "GEAS", "Electronics >70"]; where track is constant as Instrumentation and hometown Luzon
# Use .loc to filter and select columns in one step
Instru = df.loc[ 
    (df['Electronics'] > 70) & (df['Hometown'] == 'Luzon') & (df['Track'] == 'Instrumentation'),
    ['Name', 'GEAS', 'Electronics']]
Instru

#Computing the average score across the specified columns for each student
df['Average'] = df ['Math', 'Electronics', 'GEAS'].mean(axis=1)
df

# b. Filename: Mindy = ["Name", "Track", "Electronics", "Average >= 55"]; where hometown is constant as Mindanao and gender Female
# Use .loc to filter and select columns in one step
Mindy = df.loc[
    (df['Average'] >= 55) & (df['Hometown'] == 'Mindanao') & (df['Gender'] == 'Female'),
    ['Name', 'Track', 'Electronics', 'Average']]
Mindy

# End
```
2. Create a visualization that shows the different features contributes to average grade. Does chosen track in college, gender, or hommetown contributes to a higher average score?

Code:
```python
# Start

import seaborn as sns 
import matplotlib.pyplot as plt

# Getting the average score across relevant columns
df['Average'] = df[['Math', 'Electronics', 'GEAS']].mean(axis=1)

def plot_all_scores(df, columns, hue='Gender'):
    for col in columns:
        sns.barplot(x='Track', y=col, hue=hue, data=df, palette=['blue', 'black'])
        plt.title(f'{col} Scores by Track and {hue}')
        plt.show()

        sns.barplot(x='Hometown', y=col, hue=hue, data=df, palette=['orange','red'])
        plt.title(f'{col} Scores by Hometown and {hue}')
        plt.show()

#Generating the plots
plot_all_scores(df, ['Math', 'Electronics', 'GEAS'])

# End
```
   
