
# Python Exploratory Data Analysis on Spotify 2023 Dataset 
(Still In Progress)
#### JOSE MARTIN SJ. NINOBLA
#### 2 ECE - D

This repository contains Exploratory Data Analysis on Spotify 2023 Dataset for the course *Advanced Computer Programming and Algorithms (ECE 2112)* at the University of Santo Tomas, Faculty of Engineering. The experiment focuses on using Python's Pandas library for data analysis, Matplot and Seaborn for better analyzation and presentation of data.

## Project Overview
This project aims to analyze, visualize, and interpret a dataset of music tracks to extract meaningful insights about track popularity and musical trends. The analysis involves exploring track features, identifying trends in release patterns, examining relationships between musical characteristics and popularity, and generating recommendations based on findings.

## Objectives
### 1. Understand the Dataset Structure
- Load and inspect the dataset, checking for missing values, data types, and the general structure.
  
### 2. Clean and Prepare Data
- Convert columns to appropriate data types and handle missing values to ensure accurate analysis.

### 3. Compute Summary Statistics
- Provide descriptive statistics on key metrics like streams, release dates, and musical attributes (e.g., BPM, danceability).

### 4. Explore Data with Visualizations
- Create charts (bar plots, histograms, scatter plots) to uncover trends and patterns in streaming data, release dates, artist frequency, and musical attributes.

### 5. Perform Correlation Analysis
- Analyze correlations between streams and other musical attributes (like BPM, energy, danceability) to determine what factors may influence popularity.

### 6. Analyze Trends in Release Patterns
- Investigate the distribution of track releases over time, identifying any yearly or monthly patterns.

### 7. Identify Popular Tracks and Artists
- Highlight the most-streamed tracks and frequently occurring artists, exploring what makes them stand out.

### 8. Insights and Recommendations
- Based on the analysis, provide insights and recommendations about music trends, characteristics of popular tracks, and artist patterns.


## Guide Problems

### 1. Overview of Dataset
- How many rows and columns does the dataset contain?
- What are the data types of each column? Are there any missing values?

### 2. Basic Descriptive Statistics
- What are the mean, median, and standard deviation of the streams column?
- What is the distribution of released_year and artist_count? Are there any noticeable trends or outliers?

### 3. Top Performers
- Which track has the highest number of streams? Display the top 5 most streamed tracks.
- Who are the top 5 most frequent artists based on the number of tracks in the dataset?

### 4. Temporal Trends
- Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.
- Does the number of tracks released per month follow any noticeable patterns? Which month sees the most releases?

### 5. Genre and Music Characteristics
- Examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. Which attributes seem to influence streams the most?
- Is there a correlation between danceability_% and energy_%? How about valence_% and acousticness_%?

### 6. Platform Popularity
- How do the numbers of tracks in spotify_playlists, spotify_charts, and apple_playlists compare? Which platform seems to favor the most popular tracks?

### 7. Advanced Analysis
- Based on the streams data, can you identify any patterns among tracks with the same key or mode (Major vs. Minor)?
- Do certain genres or artists consistently appear in more playlists or charts? Perform an analysis to compare the most frequently appearing artists in playlists or charts.

___
### PROBLEM 1: Overview of Dataset

```python

import pandas as pd

# Load the CSV file into a DataFrame
df = pd.read_csv('spotify-2023.csv',encoding='latin1')

# Displays a summary of the DataFrame's structure, including the index range, column names, non-null counts, data types, and memory usage.
df.info()

# This calculates total number of missing (NaN) values for each column in the DataFrame and is placed in missing_values.
missing_values1 = df.isnull().sum()

# This prints out missing_values.
print(missing_values1)
```
#### Explanation:
- **`pd.read_csv()`**: Loads the dataset from a CSV file into a DataFrame named `df`.
- **`df.info()`**: Displays a summary of the DataFrame's structure, including the index range, column names, non-null counts, data types, and memory usage.
- **`missing_values1 = df.isnull().sum()`**: This calculates total number of missing (NaN) values for each column in the DataFrame and is placed in missing_values.
- **`print(missing_values1)`**: This prints out missing_values.

 ###### Note: encoding='latin1' is required to load the given dataset since the given file is not using a default UTF-8 encoding. The latin1 encoding can handle a wider range of byte values and is often used for files with Western European characters which is useful in loading this dataset.
  ___

  ### Solving Identified Problems: Data Cleaning
  Note: These 2 pairs of code are used to check the results after removing the duplicates and the null values
- **`missing_values2 = df.isnull().sum()`**
- **`print(missing_values2)`**

- **`missing_values3 = df.isnull().sum()`**
- **`print(missing_values3)`**

#### 1. Identifying and Displaying Duplicates
```python
# Identifies and removes duplicate rows based on artist and track names
dup = df[df.duplicated(['artist(s)_name', 'track_name'])]  # Finds duplicates
print("Duplicate tracks in this dataset are: ")
print(dup)  # Displays duplicate rows found
```
Code: **`dup = df[df.duplicated(['artist(s)_name', 'track_name'])]`**

Function: Finds rows with duplicate artist(s)_name and track_name and stores them in dup.
Purpose: Identifies duplicates for review before removal.

#### 2. Sorting and Removing Duplicates (Keeping the Best One):
```
df.sort_values(by=['artist(s)_name', 'track_name', 'streams', 'in_spotify_playlists'], ascending=[True, True, False, False], inplace=True)
df = df.drop_duplicates(subset=['artist(s)_name', 'track_name'], keep='first')  # Drops duplicates
```
Code: **`df.sort_values(...)`**

- Function: Sorts by artist(s)_name, track_name, streams, and in_spotify_playlists, prioritizing the highest values.
- Purpose: Ensures the best (highest streams and playlists) track is kept.

Code: **`df = df.drop_duplicates(subset=['artist(s)_name', 'track_name'], keep='first')`**

- Function: Drops duplicates, keeping the first occurrence (highest value from sorting).
- Purpose: Retains the most relevant track, removing redundant duplicates.
Note: These were used these to check the results on missing values
**`missing_values2 = df.isnull().sum()`** 
**`print(missing_values2)`**


#### 3. Data Type Conversion: Converts columns with commas to integers
```
df['in_deezer_playlists'] = df['in_deezer_playlists'].str.replace(',', '', regex=False).astype('int64')
df['streams'] = pd.to_numeric(df['streams'], errors='coerce')  # Converts streams to numeric type
df['in_shazam_charts'] = pd.to_numeric(df['in_shazam_charts'], errors='coerce')
```

Code: **`df['in_deezer_playlists'] = df['in_deezer_playlists'].str.replace(',', '', regex=False).astype('int64')`**
Function: Removes commas and converts in_deezer_playlists to integers.
Purpose: Cleans data to ensure numeric values for analysis.

Code: **`df['streams'] = pd.to_numeric(df['streams'], errors='coerce')`**
Function: Converts streams to numeric values, coercing errors into NaN.
Purpose: Ensures streams is numeric for further analysis.

Code: **`df['in_shazam_charts'] = pd.to_numeric(df['in_shazam_charts'], errors='coerce')`**

- Function: Converts in_shazam_charts to numeric values, handling errors as NaN.
- Purpose: Ensures in_shazam_charts is numeric for consistency.


#### 4. Cleaning of Null Values
```
df = df.dropna()
missing_values3 = df.isnull().sum()
print(missing_values3)
```
Dropping Rows with Missing Values:
Code: **`df = df.dropna()`**
- Function: Removes any rows in the DataFrame df that contain missing (NaN) values.
- Purpose: Cleans the dataset by dropping rows with incomplete data.
- 
Checking Remaining Missing Values:
Code: **`missing_values3 = df.isnull().sum()`**
- Function: Calculates the number of missing values (NaN) for each column in the DataFrame df after the dropna() operation.
- Purpose: Checks if any missing values remain in the dataset after dropping rows.

Code: **`print(missing_values3)`**
- Function: Prints the count of missing values for each column.
- Purpose: Displays the results to verify if any missing data is left.

Note: These were used to check the results on missing values
**`missing_values3 = df.isnull().sum()`** 
**`print(missing_values3)`**


Sorting for better visualization on the next problem:
```
df = df.sort_values(by='streams', ascending = False).reset_index(drop=True)
df
```
Code: **`df = df.sort_values(by='streams', ascending=False).reset_index(drop=True)`**
- Function: Sorts the DataFrame df by the streams column in descending order and resets the index, dropping the old index.
- Purpose: Organizes the dataset by streams, from highest to lowest, and resets the index for cleaner data.

___

### PROBLEM 2: Basic Descriptive Statistics
```python

print('dtype: ',df['streams'].dtype) #Shows the data type
# Calculates mean, median, and standard deviation of streams
mean = df['streams'].mean()
median = df['streams'].median()
std = df['streams'].std()
# Prints the mean median and std
print('mean:', mean)
print('median:', median)
print('std:', std)
```
##### Printing the Data Type of streams Column:
Code: **`print('dtype: ', df['streams'].dtype)`**
- Function: Displays the data type of the streams column in the DataFrame df.
- Purpose: To check the type of data stored in the streams column (e.g., integer, float).

##### Calculating Statistics (Mean, Median, Standard Deviation):
Code: **`mean = df['streams'].mean()`**
- Function: Calculates the mean (average) of the streams column.
- Purpose: To determine the average number of streams across all entries.

Code: **`median = df['streams'].median()`**
- Function: Calculates the median of the streams column.
- Purpose: To find the middle value of streams when the data is sorted.

Code: **`std = df['streams'].std()`**
- Function: Calculates the standard deviation of the streams column.
- Purpose: To measure the variability or spread of the streams data.

##### Printing the Calculated Statistics:
Code: **`print('mean:', mean)`**
- Function: Prints the calculated mean of the streams column.
- Purpose: Displays the average number of streams.
Code: **`print('median:', median)`**

- Function: Prints the calculated median of the streams column.
- Purpose: Displays the middle value of the streams column.
Code: print('std:', std)

- Function: Prints the calculated standard deviation of the streams column.
- Purpose: Displays the variability of the streams data.

```python

# Chart for the 'released_year'
sns.histplot(df['released_year'], kde=True)
plt.title("Distribution of Released Year")
plt.xlabel("Released Year")
plt.show()

# Chart for the 'artist_count'
sns.histplot(df['artist_count'], kde=True)
plt.title("Distribution of Artist Count")
plt.xlabel("Artist Count")
plt.show()
```

##### Chart for released_year:
Code: **`sns.histplot(df['released_year'], kde=True)`**

Function: Creates a histogram of the released_year column with a Kernel Density Estimate (KDE) curve overlay.
Purpose: To visualize the distribution of the release years of tracks in the dataset and to see trends or patterns.

Code: **`plt.title("Distribution of Released Year")`**
- Function: Sets the title of the plot.
- Purpose: To give context to the chart by labeling it as the "Distribution of Released Year".

Code: **`plt.xlabel("Released Year")`**
- Function: Sets the label for the x-axis.
- Purpose: To clarify that the x-axis represents the year the tracks were released.

Code: **`plt.show()`**
- Function: Displays the chart.
- Purpose: To render the plot and make it visible.

##### Chart for artist_count:
Code: **`sns.histplot(df['artist_count'], kde=True)`**
- Function: Creates a histogram of the artist_count column with a KDE curve overlay.
- Purpose: To visualize the distribution of the number of artists per track and understand how tracks are distributed across artists.

Code: **`plt.title("Distribution of Artist Count")`**
- Function: Sets the title of the plot.
- Purpose: To label the chart as the "Distribution of Artist Count".

Code: **`plt.xlabel("Artist Count")`**
- Function: Sets the label for the x-axis.
- Purpose: To make it clear that the x-axis represents the number of artists associated with each track.

Code: **`plt.show()`**
- Function: Displays the chart.
- Purpose: To render and show the plot of artist count distribution.
___
### PROBLEM 3: Basic Descriptive Statistics
