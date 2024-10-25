# Song Popularity Prediction

## Introduction
Music is essential to human life, influencing emotions, behavious, and even social trends. Understanding the trends and factors that drive the popularity of music is crucial for producers and musicians, enabling them to create songs that have a wide appeal to listeners. 

This study utilise a dataset initially obtained from Kaggle, comprising two files with a total of 603 entries, each of which represented a well-known song from **Spotify**. The target variable in this analysis is "**popularity**," while the predictors include "**bpm**" (tempo in beats per minute), "**dB**" (average loudness in decibels), "**energy**," "**danceability**," "**liveness**," "**valence**," "**duration**" (length of the recording in seconds), "**acousticness**, " and "**speechiness**." Given that all variables are numeric, regression analysis is appropriate for predicting music popularity.

This report will run on **KNIME** to develop and compare two regression models: **Gradient Boosting Regression** and **Random Forest Regression**. The goal is to build an accurate predictive model and evaluate the performance of these two methods in predicting the popularity of music.

<br >

## Exploratory Data Analysis (EDA)
### Distribution of Target Variable
The data indicates that most songs are quite popular, with the majority having a popularity score over 59. The mean popularity score is 66.521, indicating a negatively skewed distribution. This imbalance suggests that most songs in the dataset are relatively popular.

<img align="center" width="1104" alt="distribution of popularity" src="https://github.com/user-attachments/assets/e40b5e97-03ca-47e1-9796-cadb892738ce">

<br >
<br >

### Missing Values
Checking for missing values in the dataset is a critical step in EDA. Understanding the extent and nature of missing data helps determine the appropriate handling method. In this dataset, the missing values are minimal. In particular, there are 92 missing values for the variable "dB", 57 for "danceability", and 92 for "duration". each of these variables has less than 30% missing values, allowing for efficient imputation or alternative handling methods. 


<img align="center" width="1104" alt="missing value" src="https://github.com/user-attachments/assets/9f0b65cd-0a92-4e06-8bba-ed5b885e3791">

<br >
<br >

### Correlation Analysis and Scatter Plot
The correlation matrix and scatter plot reveal modrate correlations between features and "popularity", such as “energy” and “danceability” positively, and “acousticness” negatively. However, many features show weak linear associations with "popularity," suggesting an interaction that may be difficult to fully express with a simple linear regression. These insights justify the use of advanced regression models like non-linear regression will be bettwe suited for handling non-linear interactions and improving predicitve accuracy.

<img width="350" alt="correlation matrix" src="https://github.com/user-attachments/assets/26b064c1-e9cf-4d0a-9358-e18230e4ad55">
<p> </p>
<img align="center" width="1104" alt="scatter plot matrix" src="https://github.com/user-attachments/assets/6b2d57da-1c6a-4ffb-b5d0-2a713a5f0935">







