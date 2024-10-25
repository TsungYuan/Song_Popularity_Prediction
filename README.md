# Song Popularity Prediction

## Introduction
Music is an essential part of human, influencing emotions, behavious, and even social trends. Understanding the trends and factors that drive the popularity of music is curcial for producers and nusicians, enablibg them to create songs that have a wide appeal to listeners. 

This study utilise a dataset initially obtained from Kaggle, comprising two files with tatal of 603 entries, each of which represented a well-known song from **Spotify**. The target variable in this analysis is "**popularity**," while the predictors include "**bpm**" (tempo in beats per minute), "**dB**" (average loudness in decibels), "**energy**," "**danceability**," "**liveness**," "**valence**," "**duration**" (length of the recording in seconds), "**acousticness**, " and "**speechiness**." Given that all variables are numeric, regression analysis is apporiate for predicting music popularity.

In this report, it will develop and compare two regression models: **Gradient Boosting Regression** and **Random Forest Regression**. The goal is to build an accurate predictive model and evaluate the preformance of these two methods in predicting the popularity of music.

