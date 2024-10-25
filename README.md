# Song Popularity Prediction

## Introduction
Music is essential to human life, influencing emotions, behavious, and even social trends. Understanding the trends and factors that drive the popularity of music is crucial for producers and musicians, enabling them to create songs that have a wide appeal to listeners. 

This study utilise a dataset initially obtained from Kaggle, comprising two files with total of 603 entries, each of which represented a well-known song from **Spotify**. The target variable in this analysis is "**popularity**," while the predictors include "**bpm**" (tempo in beats per minute), "**dB**" (average loudness in decibels), "**energy**," "**danceability**," "**liveness**," "**valence**," "**duration**" (length of the recording in seconds), "**acousticness**, " and "**speechiness**." Given that all variables are numeric, regression analysis is appropriate for predicting music popularity.

This report will run on **KNIME** to develop and compare two regression models: **Gradient Boosting Regression** and **Random Forest Regression**. The goal is to build an accurate predictive model and evaluate the performance of these two methods in predicting the popularity of music.


