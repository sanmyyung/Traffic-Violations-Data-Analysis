# Traffic Violations Data Analysis

In this project, I analyzed a traffic stop dataset to explore patterns related to gender, age, violation types, and other variables. Using Python and Pandas, I investigated key questions around who gets stopped, searched, and how long stops last. This analysis provides insights into how different demographics experience traffic stops.

### Key Commands

Here’s a summary of the commands I used to analyze the data:

- `import pandas as pd`: To bring in the Pandas library.
- `pd.read_csv`: For loading the CSV file.
- `head()`: To peek at the first few rows of the data.
- `df.isnull().sum()`: To check for missing values in each column.
- `df.drop('column_name')`: To drop columns that aren’t useful (like those filled with null values).
- `value_counts`: To count occurrences of unique values in a column.
- `df.groupby('Col1')['Col2'].sum()`: Group data by one column and sum values in another.
- `df['Column_name'].map({old1:new1, old2:new2})`: To replace old values with new ones in a column.
- `df['Column_name'].mean()`: To calculate the mean of a column.
- `df.groupby('Col1')['Col2'].describe()`: To show stats summaries for data grouped by a certain column.

## Project Questions and My Solutions

### 1. Removing the Column with Only Missing Values
The first task was to identify and remove any columns filled entirely with null values. In this dataset, the `country_name` column was empty, so I removed it with:
```python
data.drop(columns='country_name', inplace=True)
```

![]()
### 2. For Speeding, Were Men or Women Stopped More Often?
To examine if there was a gender pattern in speeding stops, I filtered the data specifically for speeding violations and counted stops by gender:
```python
speeding_df = data[data['violation'] == 'Speeding']
gender_counts = speeding_df['driver_gender'].value_counts()
```

![]()
**Result:** Men were stopped more often for speeding.

### 3. Does Gender Affect Who Gets Searched During a Stop?
I investigated whether gender influences the likelihood of a search during a traffic stop. By grouping the data by gender, I compared the counts of searches conducted for men and women:

```python
data.groupby('driver_gender').search_conducted.sum()
```

![]()
**Result:** Men were more likely to be searched than women.

### 4. What is the Mean Stop Duration?
To calculate the average duration of traffic stops, I first converted the `stop_duration` values into numeric equivalents. Then, I calculated the mean:

```python
data['stop_duration'] = data['stop_duration'].map({'0-15 Min': 7.5, '16-30 Min': 24, '30+ Min': 45})
mean_stop_duration = data['stop_duration'].mean()
```

![]()
Mean Stop Duration: 12.19 minutes.

### 5. Compare the Age Distributions for Each Violation
To understand age distributions across different violation types, I grouped the data by violation type and generated descriptive statistics for driver age:

```python
data.groupby('violation')['driver_age'].describe()
```

![]()
This provided insights into age trends associated with each type of violation.

### Conclusion
This analysis highlights some intriguing trends: men are more frequently stopped for speeding, men are more likely to be searched, and there are variations in age distributions across different violations. This data could offer valuable insights for traffic policy and enforcement strategies.
