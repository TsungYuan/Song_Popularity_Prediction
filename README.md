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
The correlation matrix and scatter plot reveal modrate correlations between features and "popularity", such as “**energy**” and “**danceability**” positively, and “**acousticness**” negatively. However, many features show weak linear associations with "popularity," suggesting an interaction that may be difficult to fully express with a simple linear regression. These insights justify the use of advanced regression models like non-linear regression will be bettwe suited for handling non-linear interactions and improving predicitve accuracy.

<p> 
  <img width="350" alt="correlation matrix" src="https://github.com/user-attachments/assets/26b064c1-e9cf-4d0a-9358-e18230e4ad55">
  <p> </p>
  <img align="center" width="1104" alt="scatter plot matrix" src="https://github.com/user-attachments/assets/6b2d57da-1c6a-4ffb-b5d0-2a713a5f0935">
</p>

<br >

## Experimential Setup
### Partitioning and Pre-procedding Data
It is imperative to divide the data into training and testing sets before starting the pre-processing steps. This procedure is essential to maintain consistency in preprocessing, prevent data leakage, and guarantee an unbiased evaluation of the model's performance. This report separated the data into 80% for training and 20% for testing. 

Effectively managing missing values is crucial for maintaining dataset integrity and model accuracy. In this analysis, the features with missing values did not exceed over 30% which is relatively low (dB, danceability, and duration), Therefore, the missing values were replaced with the mean of each feature. This was done methodically by utilising KNIME's "**Missing Value**" node, which preserved the dataset's structure for further analysis.

Handling outliers is cri-cal for improving model accuracy. For this study, to enhance the predictive model's
performance, outliers were removed using the "**Numeric Outliers**" node in KNIME, ensuring that only meaningful data points contribute to the model's training process.

<br >
<br >

### Hyperparameter Tuning
Hyperparameter is vital for optimising the performance of predictive models.

In the hyperparameter tuning process for Random Forest Regression in KNIME, I employed the "**Parameter Optimization Loop Start**" and "**Parameter Optimization Loop End**" nodes. Key factors influencing the performance of the predictive model include tree depth, minimum node size, and the number of trees. In this study, the configurations of the hyperparameters were set as follows: the tree depth is adjusted from a start value of 5 to a stop value of 10, the number of models ranges from 70 to 150, and the minimum node size ranges from 5 to 20.

For conducting the hyperparameter tuning process for GBR in KNIME, I utilised the same nodes as used for Random Forest Regression. The key factors influencing the performance of the GBR model include the learning rate, the number of trees, and the tree depth. Accordingly, the hyperparameters were configured as follows: the learning rate is varied from 0.1 to 1.0, the tree depth ranges from 2 to 6, and the number of trees ranges from 70 to 170. These parameters were systematically adjusted within the specified ranges to identify the optimal configuration that maximizes the model's performance.

<br >
<br >

### Cross-Validation
The process for implementing cross-validation for both predictive models in KNIME involves utilising the "**X-Partitioner**" and "**X-Aggregator**" nodes. Cross-validation was applied during both the hyperparameter tuning process and the final predictive modelling to ensure model robustness. Specifically, a 5-fold cross-validation was used during hyperparameter tuning to reduce processing time, while a 10-fold cross-validation was employed for the final predictive model to ensure robustness and generalizability. This dual-stage approach ensures that the models were both efficient and reliable.





