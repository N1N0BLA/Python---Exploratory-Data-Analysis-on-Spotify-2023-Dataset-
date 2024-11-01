
# Python Exploratory Data Analysis on Spotify 2023 Dataset
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
