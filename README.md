
# 🌟Python Exploratory Data Analysis on Spotify 2023 Dataset 
## JOSE MARTIN SJ. NINOBLA | 2 ECE - D


## 🎓Course
**ECE 2112: Advanced Computer Programming and Algorithms**

## 🏫 University
**University of Santo Tomas**  
**Faculty of Engineering**  
**Electronics Engineering Department**  

## 📅 Academic Year
**First Term, AY 2024 – 2025**

This repository contains Exploratory Data Analysis on Spotify 2023 Dataset for the course *Advanced Computer Programming and Algorithms (ECE 2112)* at the University of Santo Tomas, Faculty of Engineering. The experiment focuses on using Python's Pandas library for data analysis, Matplot and Seaborn for better analyzation and presentation of data.

## 🚀Project Overview
This project aims to analyze, visualize, and interpret a dataset of music tracks to extract meaningful insights about track popularity and musical trends. The analysis involves exploring track features, identifying trends in release patterns, examining relationships between musical characteristics and popularity, and generating recommendations based on findings.

## 📚 Table of Contents

1. [Objectives](#-objectives)
2. [Guide Problems](-#guide-problems)
3. [Installation](#how-to-run)
4. [Requirements](#requirements)
5. [PROBLEM 1](#-problem-1)
6. [PROBLEM 2](#-problem-2)
7. [PROBLEM 3](#-problem-3)
8. [PROBLEM 4](#-problem-4)
9. [PROBLEM 5](#-problem-5)
10. [PROBLEM 6](#-problem-6)
11. [PROBLEM 7](#-problem-7)


## 📑 Objectives
#### 1. Understand the Dataset Structure
- Load and inspect the dataset, checking for missing values, data types, and the general structure.
  
#### 2. Clean and Prepare Data
- Convert columns to appropriate data types and handle missing values to ensure accurate analysis.

#### 3. Compute Summary Statistics
- Provide descriptive statistics on key metrics like streams, release dates, and musical attributes (e.g., BPM, danceability).

#### 4. Explore Data with Visualizations
- Create charts (bar plots, histograms, scatter plots) to uncover trends and patterns in streaming data, release dates, artist frequency, and musical attributes.

#### 5. Perform Correlation Analysis
- Analyze correlations between streams and other musical attributes (like BPM, energy, danceability) to determine what factors may influence popularity.

#### 6. Analyze Trends in Release Patterns
- Investigate the distribution of track releases over time, identifying any yearly or monthly patterns.

#### 7. Identify Popular Tracks and Artists
- Highlight the most-streamed tracks and frequently occurring artists, exploring what makes them stand out.

#### 8. Insights and Recommendations
- Based on the analysis, provide insights and recommendations about music trends, characteristics of popular tracks, and artist patterns.


##🧾 Guide Problems

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
## 🚩 PROBLEM 1
### Overview of Dataset

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
  ###### Note: These 2 pairs of code are used to check the results after removing the duplicates and the null values
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
- Function: Finds rows with duplicate artist(s)_name and track_name and stores them in dup.
- Purpose: Identifies duplicates for review before removal.

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
- Function: Removes commas and converts in_deezer_playlists to integers.
- Purpose: Cleans data to ensure numeric values for analysis.

Code: **`df['streams'] = pd.to_numeric(df['streams'], errors='coerce')`**
- Function: Converts streams to numeric values, coercing errors into NaN.
- Purpose: Ensures streams is numeric for further analysis.

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

## 🚩 PROBLEM 2
### Basic Descriptive Statistics
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
  
Code: **`print('std:', std)`**
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
- Function: Creates a histogram of the released_year column with a Kernel Density Estimate (KDE) curve overlay.
- Purpose: To visualize the distribution of the release years of tracks in the dataset and to see trends or patterns.

Code: **`plt.title("Distribution of Released Year")`**
- Function: Sets the title of the plot.
- Purpose: To give context to the chart by labeling it as the "Distribution of Released Year".

Code: **`plt.xlabel("Released Year")`**
- Function: Sets the label for the x-axis.
- Purpose: To clarify that the x-axis represents the year the tracks were released.

Code: **`plt.show()`**
- Function: Displays the chart.
- Purpose: To render the plot and make it visible.

### 📊 CHART ANALYSIS:
- **Main Pattern**: The "Released Year" distribution shows a sharp increase in the number of releases over time, particularly after 2000. This indicates that most releases are recent, with a significant concentration of releases occurring from 2010 onward.
- **Trend**: There's a steep rise in releases starting around 2020, suggesting a possible increase in content production or data coverage for more recent years.
- **Outliers**: The spike in releases in the last few years (around 2020-2022) stands out as an outlier in comparison to previous decades. This may indicate a trend of rapidly increasing content production in recent years, possibly due to the rise of digital platforms and streaming services.
  
##### 📊 Chart for artist_count:
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
  
#### 📊 CHART ANALYSIS:
- **Main Pattern**: The "Artist Count" distribution is right-skewed, with the majority of releases featuring only a single artist. This is indicated by the peak at an artist count of 1.
- **Trend**: There is a decreasing frequency as the artist count increases, showing that releases with more artists are less common.
- **Outliers**: There are some releases with a high artist count (5 or more), but they are quite rare, and these points could be considered outliers. These outliers may represent collaborations or ensemble works.



___
## 🚩 PROBLEM 3
#### Basic Descriptive Statistics
**Sorting and Displaying Top 5 Most Streamed Tracks:**
```python

# Sort the dataset by 'streams' in descending order and select the top 5 tracks
top_streamed_tracks = df.sort_values(by='streams', ascending=False).head(5)

# Display the top 5 most streamed tracks with relevant information
print("Top 5 Most Streamed Tracks:")
print(top_streamed_tracks[['track_name', 'artist(s)_name', 'streams']])

```
Code: **`top_streamed_tracks = df.sort_values(by='streams', ascending=False).head(5)`**
- Function: Sorts the DataFrame df by the streams column in descending order and selects the top 5 tracks.
- Purpose: To identify the 5 tracks with the highest number of streams.

Code: **`print("Top 5 Most Streamed Tracks:")`**
Function: Prints a header to label the output for top streamed tracks.
Purpose: To give context to the printed list of top streamed tracks.

Code: **`print(top_streamed_tracks[['track_name', 'artist(s)_name', 'streams']])`**
- Function: Displays the track_name, artist(s)_name, and streams for the top 5 streamed tracks.
- Purpose: To show the names and streaming counts of the top 5 most streamed tracks.

**Counting and Displaying Top 5 Most Frequent Artists:**
```python

# Count the occurrences of each artist and select the top 5
top_artists = df['artist(s)_name'].value_counts().head(5)

# Display the top 5 most frequent artists
print("Top 5 Most Frequent Artists by Number of Tracks:")
print(top_artists)

```
Code: **`top_artists = df['artist(s)_name'].value_counts().head(5)`**
- Function: Counts the occurrences of each artist in the artist(s)_name column and selects the top 5 artists with the most tracks.
- Purpose: To find the artists who have the most tracks in the dataset.

Code: **`print("Top 5 Most Frequent Artists by Number of Tracks:")`**
- Function: Prints a header to label the output for top frequent artists.
- Purpose: To introduce the list of top 5 artists by track count.

Code: **`print(top_artists)`**
- Function: Prints the list of top 5 most frequent artists and their respective track counts.
- Purpose: To display the top 5 artists based on the number of tracks they have in the dataset.

 ___
## 🚩 PROBLEM 4
#### Temporal Trends
**Plotting the Number of Tracks Released Per Year:**
```python

# Group by 'released_year' and count the number of tracks per year
tracks_per_year = df.groupby('released_year').size()

# Plot the number of tracks released per year
plt.figure(figsize=(10, 6))
tracks_per_year.plot(kind='line', marker='o')
plt.title("Number of Tracks Released Per Year")
plt.xlabel("Year")
plt.ylabel("Number of Tracks")
plt.grid()
plt.show()
```
Code: **`tracks_per_year = df.groupby('released_year').size()`**
- Function: Groups the DataFrame df by released_year and counts the number of tracks for each year.
- Purpose: To determine how many tracks were released each year.

Code: **`tracks_per_year.plot(kind='line', marker='o')`**
- Function: Creates a line plot showing the number of tracks released per year.
- Purpose: To visualize the trend in the number of tracks released over time.

Code: **`plt.title("Number of Tracks Released Per Year")`**
- Function: Sets the title of the plot.
- Purpose: To give context to the plot, indicating that it shows the number of tracks released per year.

Code: **`plt.xlabel("Year")`**
- Function: Sets the label for the x-axis.
- Purpose: To clarify that the x-axis represents the year of release.

Code: **`plt.ylabel("Number of Tracks")`**
- Function: Sets the label for the y-axis.
- Purpose: To clarify that the y-axis represents the number of tracks.

Code: **`plt.grid()`**
- Function: Adds a grid to the plot for better readability.
- Purpose: To improve the visual clarity of the plot.

Code: **`plt.show()`**
- Function: Displays the plot.
- Purpose: To render and show the plot of the number of tracks released per year.


**Plotting the Number of Tracks Released Per Month:**
```python

import calendar

# Map numbers 1-12 to month names
df['released_month'] = df['released_month'].apply(lambda x: calendar.month_name[x])

# Group by 'released_month' and count the number of tracks per month
tracks_per_month = df['released_month'].value_counts().reindex(calendar.month_name[1:])

# Plot the number of tracks released per month
plt.figure(figsize=(10, 6))
tracks_per_month.plot(kind='bar', color='skyblue')
plt.title("Number of Tracks Released Per Month")
plt.xlabel("Month")
plt.ylabel("Number of Tracks")
plt.xticks(rotation=45)
plt.show()


```
Code: **`df['released_month'] = df['released_month'].apply(lambda x: calendar.month_name[x])`**
- Function: Maps the month number (1-12) in the released_month column to the corresponding month name using the calendar library.
- Purpose: To convert numeric month values into readable month names (e.g., 1 → January, 2 → February).

Code: **`tracks_per_month = df['released_month'].value_counts().reindex(calendar.month_name[1:])`**
- Function: Counts the occurrences of each month name in released_month and orders the result by month (from January to December).
- Purpose: To determine how many tracks were released in each month of the year.

Code: **`tracks_per_month.plot(kind='bar', color='skyblue')`**
- Function: Creates a bar plot showing the number of tracks released per month.
- Purpose: To visualize the distribution of track releases across different months of the year.

Code: **`plt.title("Number of Tracks Released Per Month")`**
- Function: Sets the title of the plot.
- Purpose: To provide context for the chart, indicating it shows the number of tracks released each month.

Code: **`plt.xlabel("Month")`**
- Function: Sets the label for the x-axis.
- Purpose: To clarify that the x-axis represents the months of the year.

Code: **`plt.ylabel("Number of Tracks")`**
- Function: Sets the label for the y-axis.
- Purpose: To clarify that the y-axis represents the number of tracks released.

Code: **`plt.xticks(rotation=45)`**
- Function: Rotates the x-axis tick labels by 45 degrees for better readability.
- Purpose: To prevent overlap of the month names on the x-axis.

Code: **`plt.show()`**
- Function: Displays the plot.
- Purpose: To render and show the bar plot of the number of tracks released per month.

Identifying the Month with the Most Releases:
```python

# Identify the month with the most releases
most_releases_month = tracks_per_month.idxmax()
print(f"The month with the most releases is: {most_releases_month}")

```
Code: **`most_releases_month = tracks_per_month.idxmax()`**
- Function: Finds the month with the highest number of track releases.
- Purpose: To determine which month had the most track releases.

Code: **`print(f"The month with the most releases is: {most_releases_month}")`**
- Function: Prints the month with the most track releases.
- Purpose: To display the month that had the highest number of releases.

#### 📊 CHART ANALYSIS:
1. **Trends in the Number of Tracks Released Over Time**
- Overall Pattern: The chart on the left, "Number of Tracks Released Per Year," shows that the number of track releases remained low and relatively stable from the early 1900s until the early 2000s.
- Sharp Increase: Starting around 2010, there is a notable upward trend, with a dramatic spike after 2020. This sharp increase likely reflects either a rise in music production, a more comprehensive dataset for recent years, or a shift to digital platforms that has facilitated greater accessibility and recording frequency.
- Peak and Decline: The highest point appears to be around 2022, after which there is a slight drop. This peak could be due to data collection factors or reflect an actual decline in releases for the most recent year.

2. **Patterns in the Number of Tracks Released Per Month**
- Monthly Release Patterns: The "Number of Tracks Released Per Month" chart shows variation in releases across different months, with some months consistently seeing more releases than others.
- Most Releases in May: May has the highest number of releases, standing out above all other months. January also has a high number of releases, but it's slightly lower than May.
- Other Observations: There is no clear seasonality that would suggest that certain quarters of the year are significantly more active, though May appears to be a prominent month for releases. The summer months, particularly June, July, and August, show a slight dip in the number of releases.




 ___
## 🚩 PROBLEM 5
### Correlation Analysis and Visualizations
**Calculating and Visualizing Correlation Matrix**
```python
# relevant columns for correlation analysis
attributes = ['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']

# Calculates correlation matrix
correlation_matrix = df[attributes].corr()
# Creates a heatmap to visualize the correlation matrix
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', vmin=-1, vmax=1, 
            linewidths=0.5, fmt='.2f', cbar_kws={'label': 'Correlation Coefficient'})

# title
plt.title("Correlation Matrix of Streams and Other Musical Attributes")

# Shows the plot
plt.show()

```
Code: **`attributes = [...]`**
- Function: Defines a list of attributes/columns relevant for the correlation analysis.
- Purpose: To specify the musical attributes (e.g., streams, BPM, energy, etc.) for which correlations will be computed.

Code: **`correlation_matrix = df[attributes].corr()`**
- Function: Calculates the correlation matrix for the specified columns in the attributes list.
- Purpose: To examine how different musical attributes are related to each other, focusing on numeric correlations.

Code: **`sns.heatmap(...)`**
- Function: Creates a heatmap to visualize the correlation matrix, with values annotated, color-coded, and a legend for correlation coefficients.
- Purpose: To provide a visual representation of the strength and direction of correlations between attributes, where positive and negative correlations are shown in different colors.

Code: **`plt.title("Correlation Matrix of Streams and Other Musical Attributes")`**
- Function: Sets the title of the heatmap.
- Purpose: To describe the plot and give context to the correlation matrix visualization.

Code: **`plt.show()`**
- Function: Displays the heatmap.
- Purpose: To render the plot and make it visible.

**Calculating Specific Correlations**
```python
# Calculate correlation between danceability_% and energy_%
danceability_energy_corr = df['danceability_%'].corr(df['energy_%'])
print(f"Correlation between danceability_% and energy_%: {danceability_energy_corr}")

# Calculate correlation between valence_% and acousticness_%
valence_acousticness_corr = df['valence_%'].corr(df['acousticness_%'])
print(f"Correlation between valence_% and acousticness_%: {valence_acousticness_corr}")

```
Code: **`danceability_energy_corr = df['danceability_%'].corr(df['energy_%'])`**

- Function: Calculates the correlation between danceability_% and energy_%.
- Purpose: To check how danceability is related to energy in the dataset.

Code: **`valence_acousticness_corr = df['valence_%'].corr(df['acousticness_%'])`**
- Function: Calculates the correlation between valence_% and acousticness_%.
- Purpose: To analyze the relationship between valence (mood) and acousticness (level of acoustic sound) of the tracks.

Code: **`print(...)`**
- Function: Prints the calculated correlation values for the specific musical attribute pairs.
- Purpose: To display the correlation values in the console for interpretation.

**Heatmap Visualization**
Code:**`plt.figure(figsize=(8, 6))`**
- Function: Initializes the plot with a figure size of 8 by 6 inches.
- Purpose: To set the dimensions of the plot for better clarity and presentation.

Code: **`sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)`**
- Function: Generates a heatmap from the correlation_matrix using the seaborn library.
- **`annot=True`**: Annotates each cell with the correlation coefficient values.
- **`cmap='coolwarm'`**: Specifies the color scheme (blue for negative correlations, red for positive correlations).
- **`center=0`**: Centers the color palette around 0, ensuring that neutral correlations (0) are represented by a neutral color (e.g., white or gray).
- Purpose: To visually represent the strength and direction of the correlation between various musical attributes (such as streams, energy, danceability, etc.) in the dataset. Positive correlations are shown in shades of red, while negative correlations are in blue, making it easy to identify relationships.

Code:**` plt.title("Correlation Matrix for Streams and Musical Attributes")`**
- Function: Adds a title to the heatmap plot.
- Purpose: To label the plot and provide context, explaining that the plot represents the correlation matrix for streams and other musical attributes.

Code: **`plt.show()`**
- Function: Displays the heatmap plot.
- Purpose: To render the plot and make it visible.


#### 📊 CHART ANALYSIS:
1. Correlation Between Streams and Musical Attributes
- **Danceability%**: The correlation between streams and danceability_% is low, with a coefficient around -0.09 in the left matrix and -0.094 in the right matrix. This suggests a weak and slightly negative relationship, indicating that higher danceability does not necessarily lead to more streams.
- **Energy%**: The energy_% attribute shows an even weaker correlation with streams, with a value of -0.04 in the left matrix and -0.036 in the right matrix. This near-zero value indicates virtually no relationship between a track’s energy level and its number of streams.
- **BPM**: The bpm attribute has a negligible correlation with streams, approximately -0.02 to -0.025 across both matrices. This minimal value shows that tempo, represented by bpm, has almost no effect on the streaming numbers.
Overall, none of these musical attributes (danceability, energy, bpm) have a strong influence on the number of streams. The weak correlations suggest that other factors beyond these musical features likely play a more significant role in determining a track’s popularity.

2. Correlation Between Danceability% and Energy%, and Valence% and Acousticness%
- Danceability% and Energy%: The correlation between danceability_% and energy_% is moderate and positive, with values around 0.16 in both matrices. This indicates that tracks with higher danceability tend to also have slightly higher energy levels, though the relationship is not strong.
- Valence% and Acousticness%: The correlation between valence_% and acousticness_% is moderate and negative, approximately -0.55 in both matrices. This negative correlation suggests that more acoustic tracks tend to have lower valence (less positive emotion) and vice versa.




  
 ___
## 🚩 PROBLEM 6
### Playlist and Stream Correlation Analysis
Summing Tracks Across Platforms
```python
# Sum the total track count across each playlist platform
playlist_counts = {
    'Spotify': df['in_spotify_playlists'].sum(),
    'Deezer': df['in_deezer_playlists'].sum(),
    'Apple': df['in_apple_playlists'].sum()
}
# Display the total track counts for each platform
print("Total number of tracks in each platform's playlists:")
for platform, count in playlist_counts.items():
    print(f"{platform}: {count}")
# Creates a bar chart for the total track count on each platform
plt.figure(figsize=(8, 6))
plt.bar(playlist_counts.keys(), playlist_counts.values(), color=['#1DB954', '#FF2D55', '#000000'])  # Color for each platform
plt.title("Total Tracks in Playlists by Platform", fontsize=16)
plt.xlabel("Platform", fontsize=14)
plt.ylabel("Total Track Count", fontsize=14)
plt.xticks(rotation=45)
plt.tight_layout()

# Shows the plot
plt.show()

```
Code: **`playlist_counts = { ... }`**
- Function: Creates a dictionary to sum the total track count for each playlist platform (Spotify, Deezer, Apple).
- Purpose: To calculate the total number of tracks in playlists for each platform.

Code: **`print("Total number of tracks in each platform's playlists:")`**
- Function: Prints the label for displaying the total track counts.
- Purpose: To introduce the output showing the total track counts by platform.

Code: **`for platform, count in playlist_counts.items(): print(f"{platform}: {count}")
Function: Loops through the playlist_counts dictionary and prints the total track count for each platform.
Purpose: To display the total number of tracks available on each playlist platform.
Bar Chart of Total Tracks in Playlists

Code: **`plt.bar(playlist_counts.keys(), playlist_counts.values(), ...)`**
- Function: Creates a bar chart showing the total track counts for Spotify, Deezer, and Apple playlists.
- Purpose: To visually compare the total track count across platforms.

Code: **`plt.show()`**
- Function: Displays the bar chart.
- Purpose: To render the plot and make it visible.

Correlation Between Streams and Playlist Counts
```python
# Calculate the correlation between streams and each playlist platform
spotify_corr = df['streams'].corr(df['in_spotify_playlists'])
deezer_corr = df['streams'].corr(df['in_deezer_playlists'])
apple_corr = df['streams'].corr(df['in_apple_playlists'])


correlations = {
    'Spotify': spotify_corr,
    'Deezer': deezer_corr,
    'Apple': apple_corr
}

# Convert the correlations dictionary to a DataFrame for plotting
correlations_df = pd.DataFrame(list(correlations.items()), columns=['Platform', 'Correlation'])

# Plot the correlations as a bar chart
plt.figure(figsize=(8, 6))
sns.barplot(data=correlations_df, x='Platform', y='Correlation', hue='Platform', dodge=False, palette='deep', legend=False)
plt.title('Correlation between Playlist Count and Streams by Platform')
plt.ylim(-1, 1)  # Set y-axis limits to the correlation range
plt.xlabel('Platform')
plt.ylabel('Correlation with Streams')
plt.show()

# Display correlation results
print("\nCorrelation of playlist counts with streams (higher values suggest more popular track preference):")
print(f"Spotify: {spotify_corr}")
print(f"Deezer: {deezer_corr}")
print(f"Apple: {apple_corr}")

```
Code: **`spotify_corr = df['streams'].corr(df['in_spotify_playlists'])`**
- Function: Calculates the correlation between streams and in_spotify_playlists.
- Purpose: To determine how strongly streams correlate with track appearances in Spotify playlists.

Code: **`correlations = { ... }`**
- Function: Stores the correlation values between streams and playlist counts for each platform in a dictionary.
- Purpose: To summarize correlations between tracks' popularity (streams) and their playlist appearances.

Code: **`sns.barplot(data=correlations_df, ...)`**
- Function: Creates a bar chart to visualize the correlation values between each platform’s playlist count and streams.
- Purpose: To show the strength of the relationship between playlists and streams for each platform.

Code: **`print(...)`**
- Function: Displays the calculated correlations for each platform.
- Purpose: To inform the user of the exact correlation values between streams and playlist appearances on Spotify, Deezer, and Apple.

 ___
## 🚩 PROBLEM 7
### Streams by Key and Mode, Artist Playlist and Chart Appearances
Descriptive Statistics by Key and Mode
```python
# Group by 'key' and 'mode', then calculate mean, median, std, and percentiles
grouped_stats = df.groupby(['key', 'mode'])['streams'].agg(
    mean='mean',
    median='median',
    std='std',
    q25=lambda x: x.quantile(0.25),
    q75=lambda x: x.quantile(0.75)
).reset_index()

print(grouped_stats)

# Visualization
plt.figure(figsize=(12, 6))
sns.boxplot(data=df, x='key', y='streams', hue='mode', palette='Set2')
plt.title('Distribution of Streams by Key and Mode')
plt.xlabel('Key')
plt.ylabel('Streams')
plt.yscale('log')  # Log scale for better visibility
plt.legend(title='Mode')
plt.show()

```
Code: **`grouped_stats = df.groupby(['key', 'mode'])['streams'].agg(...)`**
- Function: Groups the data by key and mode, then calculates mean, median, standard deviation, and quantiles (25th and 75th percentiles) for streams.
- Purpose: To explore how streams vary across different musical keys and modes (e.g., major/minor scales).

Code: **`sns.boxplot(data=df, x='key', y='streams', hue='mode', ...)`**
- Function: Creates a box plot to visualize the distribution of streams by key and mode.
- Purpose: To compare the spread and central tendency of streams across different keys and modes.

Code: **`plt.show()`**
- Function: Displays the box plot.
- Purpose: To render and show the plot for the distribution of streams by key and mode.

### CHART USAGE: Why was a boxplot graph utilized?
- Using mean, median, standard deviation, and percentiles will give a fuller picture of the distribution within each key and mode.
- This approach lets you identify if certain keys or modes tend to have a higher median or average stream count, while also spotting high variability or skewness.
  
#### 📊 CHART ANALYSIS:
- The highest streaming numbers appear in C# and D keys, particularly in major mode
- Several keys show notable high outliers, reaching up to 10^10 streams
- Major mode generally shows higher median streams across most keys 
- F and F# keys show the lowest median streaming numbers
- Minor mode consistently shows lower streaming numbers compared to major
- The lowest streams are around 104 to 105 range

**Artist Playlist Appearances**
```python
# Assuming columns `artist` and playlist counts ('in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists') exist
# Calculate the total number of playlist appearances for each artist
df['total_playlist_appearances'] = df[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].sum(axis=1)
artist_playlist_counts = df.groupby('artist(s)_name')['total_playlist_appearances'].sum().sort_values(ascending=False).reset_index()

# Display top 10 artists with the most playlist appearances
top_artists = artist_playlist_counts.head(10)
print("Top 10 artists based on playlist appearances:")
print(top_artists)

# Plot the top 10 artists by playlist appearances
plt.figure(figsize=(10, 6))
sns.barplot(data=top_artists, x='total_playlist_appearances', y='artist(s)_name', palette='coolwarm', hue='artist(s)_name', legend=False)
plt.title('Top 10 Artists by Playlist Appearances')
plt.xlabel('Total Playlist Appearances')
plt.ylabel('Artist')
plt.show()

```
Code: **`df['total_playlist_appearances'] = df[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].sum(axis=1)`**
- Function: Calculates the total playlist appearances for each track across the three platforms (Spotify, Deezer, Apple).
- Purpose: To aggregate the number of playlists each track appears in across the specified platforms.

Code: **`top_artists = artist_playlist_counts.head(10)`**
- Function: Selects the top 10 artists based on the total playlist appearances.
- Purpose: To display the top artists with the most playlist appearances.

Code: **`sns.barplot(...)`**
- Function: Creates a bar chart displaying the top 10 artists based on total playlist appearances.
- Purpose: To visually represent which artists have the most tracks in playlists across platforms.

Code: **`plt.show()`**
- Function: Displays the bar chart.
- Purpose: To render and show the bar chart for the top 10 artists by playlist appearances.

**Artist Chart Appearances**
```python
# Assuming columns `artist` and charts counts ('in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts') exist
# Calculate the total number of playlist appearances for each artist
df['total_chart_appearances'] = df[['in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts']].sum(axis=1)
artist_playlist_counts = df.groupby('artist(s)_name')['total_chart_appearances'].sum().sort_values(ascending=False).reset_index()

# Display top 10 artists with the most playlist appearances
top_artists = artist_playlist_counts.head(10)
print("Top 10 artists based on chart appearances:")
print(top_artists)

# Plot the top 10 artists by playlist appearances
plt.figure(figsize=(10, 6))
sns.barplot(data=top_artists, x='total_chart_appearances', y='artist(s)_name', palette='coolwarm', hue='artist(s)_name', legend=False)
plt.title('Top 10 Artists by Chart Appearances')
plt.xlabel('Total Chart Appearances')
plt.ylabel('Artist')
plt.show()

```
Code: **`df['total_chart_appearances'] = df[['in_spotify_charts', 'in_apple_charts', 'in_deezer_charts', 'in_shazam_charts']].sum(axis=1)`**
- Function: Calculates the total chart appearances for each track across the four platforms (Spotify, Apple, Deezer, Shazam).
- Purpose: To aggregate the number of chart appearances each track has across the specified platforms.

Code: **`top_artists = artist_playlist_counts.head(10)`**
- Function: Selects the top 10 artists based on the total chart appearances.
- Purpose: To display the top artists with the most chart appearances.

Code: **`sns.barplot(...)`**
- Function: Creates a bar chart displaying the top 10 artists based on total chart appearances.
- Purpose: To visually represent which artists have the most tracks on charts across platforms.

Code: **`plt.show()`**
- Function: Displays the bar chart.
- Purpose: To render and show the bar chart for the top 10 artists by chart appearances.

#### 📊 CHART ANALYSIS:

##### Analysis of Artists by Playlist Appearances

- Ed Sheeran and Taylor Swift are the most prominent artists in playlists, with high appearance counts, indicating their strong presence and popularity across various user-created or algorithmic playlists.
- Other artists on this list, such as Eminem, Coldplay, and Dr. Dre (Snoop Dogg), suggest a mix of genres—ranging from pop, hip-hop, rap, rock, and electronic.
- Artists like Avicii and Daft Punk represent electronic and dance genres, which often perform well in playlist settings, possibly due to their suitability for mood-based playlists.
- Nirvana and Adele, representing rock and pop respectively, also show strong playlist appearances, indicating broad appeal across diverse listener groups.

##### Analysis of Artists by Chart Appearances
- Taylor Swift has the highest number of chart appearances by a significant margin, which suggests her consistent charting success and popularity across demographics.
- Bad Bunny and SZA are other top-charting artists, indicating the popularity of Latin music and R&B in mainstream charts.
- Newer artists like Olivia Rodrigo and NewJeans are also prominent, reflecting the influence of recent trends and younger audiences.
- A more varied genre representation is evident here with artists like Dave, Central Cee (UK rap), and Latto (hip-hop), suggesting that hip-hop and rap are well-represented in charts.
  
##### Comparing Playlist and Chart Appearances
- Taylor Swift and Ed Sheeran appear in both the playlist and chart lists, showing that they have a consistent presence across both metrics.
- Genres: Pop, hip-hop, and rap artists appear frequently in both playlists and charts, indicating that these genres have broad appeal and adaptability.
- Diverse Popularity: Some artists like Bad Bunny and SZA perform better in charts but aren't as prominent in playlists, possibly reflecting their recent surge in mainstream popularity rather than organic playlist curation.
- Electronic/Dance Music: Artists like Avicii and Daft Punk appear mainly in playlists, which may suggest that while they are popular in curated listening experiences, they might not have as consistent chart performance.

##### Conclusion
- Pop and hip-hop/rap artists consistently appear in both playlists and charts, showing their wide-reaching appeal. However, certain genres, such as electronic, seem more playlist-oriented, while newer artists or genre-specific stars (like Latin or R&B) are more prevalent in charts. This analysis highlights the evolving - - popularity dynamics between mainstream charts and curated playlists, driven by both legacy artists and rising stars.

**`df.info()`** - This is used in the last part to verify the new dataset after the cleaning and checking process.

## How to Run

1. Download and Install the Anaconda Distribution app in your Computer
   ```
   https://www.anaconda.com/download
   ```

2. Launch the Jupiter Notebook and create a new notebook
   

3. Copy Paste the codes and shift + enter to see the Output

## Requirements

- Python 3.x
- Pandas library
- Matplotlib library
- Seaborn library
