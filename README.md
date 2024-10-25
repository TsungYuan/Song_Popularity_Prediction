# Song Popularity Prediction from Spotify:  
### Random Forest Regression and Gradient Boosting Regression

## Introduction
Music is essential to human life, influencing emotions, behavious, and even social trends. Understanding the trends and factors that drive the popularity of music is crucial for producers and musicians, enabling them to create songs that have a wide appeal to listeners. 

This study utilise a dataset initially obtained from Kaggle, comprising two files with a total of 603 entries, each of which represented a well-known song from **Spotify**. The target variable in this analysis is "**popularity**," while the predictors include "**bpm**" (tempo in beats per minute), "**dB**" (average loudness in decibels), "**energy**," "**danceability**," "**liveness**," "**valence**," "**duration**" (length of the recording in seconds), "**acousticness**, " and "**speechiness**." Given that all variables are numeric, regression analysis is appropriate for predicting music popularity.

This report will run on **KNIME** to develop and compare two regression models: **Gradient Boosting Regression** and **Random Forest Regression**. The goal is to build an accurate predictive model and evaluate the performance of these two methods in predicting the popularity of music.

<br >

## Exploratory Data Analysis (EDA)
### Distribution of Target Variable
The data indicates that most songs are quite popular, with the majority having a popularity score over 59. The mean popularity score is 66.521, indicating a negatively skewed distribution. This imbalance suggests that most songs in the dataset are relatively popular.
<p>
  <img align="center" width="1104" alt="distribution of popularity" src="https://github.com/user-attachments/assets/e40b5e97-03ca-47e1-9796-cadb892738ce">
</p>

<br >

### Missing Values
Checking for missing values in the dataset is a critical step in EDA. Understanding the extent and nature of missing data helps determine the appropriate handling method. In this dataset, the missing values are minimal. In particular, there are 92 missing values for the variable "dB", 57 for "danceability", and 92 for "duration". each of these variables has less than 30% missing values, allowing for efficient imputation or alternative handling methods. 
<p>
  <img align="center" width="1104" alt="missing value" src="https://github.com/user-attachments/assets/9f0b65cd-0a92-4e06-8bba-ed5b885e3791">
</p>

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

Handling outliers is critical for improving model accuracy. For this study, to enhance the predictive model's
performance, outliers were removed using the "**Numeric Outliers**" node in KNIME, ensuring that only meaningful data points contribute to the model's training process.

<br >

### Hyperparameter Tuning
Hyperparameter is vital for optimising the performance of predictive models.

In the hyperparameter tuning process for Random Forest Regression in KNIME, I employed the "**Parameter Optimization Loop Start**" and "**Parameter Optimization Loop End**" nodes. Key factors influencing the performance of the predictive model include tree depth, minimum node size, and the number of trees. In this study, the configurations of the hyperparameters were set as follows: the tree depth is adjusted from a start value of 5 to a stop value of 10, the number of models ranges from 70 to 150, and the minimum node size ranges from 5 to 20.

For conducting the hyperparameter tuning process for GBR in KNIME, I utilised the same nodes as used for Random Forest Regression. The key factors influencing the performance of the GBR model include the learning rate, the number of trees, and the tree depth. Accordingly, the hyperparameters were configured as follows: the learning rate is varied from 0.1 to 1.0, the tree depth ranges from 2 to 6, and the number of trees ranges from 70 to 170. These parameters were systematically adjusted within the specified ranges to identify the optimal configuration that maximizes the model's performance.

<br >

### Cross-Validation
The process for implementing cross-validation for both predictive models in KNIME involves utilising the "**X-Partitioner**" and "**X-Aggregator**" nodes. Cross-validation was applied during both the hyperparameter tuning process and the final predictive modelling to ensure model robustness. Specifically, a 5-fold cross-validation was used during hyperparameter tuning to reduce processing time, while a 10-fold cross-validation was employed for the final predictive model to ensure robustness and generalizability. This dual-stage approach ensures that the models were both efficient and reliable.

<br >

## Result
To evaluate the performance of the Random Forest (RF) and Gradient Boosting Regression (GBR) models, we primarily used Mean Squared Error (MSE) and R-squared (R²). MSE measures the average squared difference between the predicted and actual values, providing insight into the prediction accuracy. R² indicates the proportion of variance in the dependent variable that is predictable from the independent variables, reflecting the model's explanatory power.

Examining the cross-validation results, it is noticeable that some folds exhibited low MSE values for both RF and GBR, indicating periods of relatively good predictive performance. However, the overall cross-validation results show a lower R² and a higher MSE, reflecting a more robust and generalized prediction performance. This outcome highlights that while individual folds may perform well, the models' ability to generalize across different data splits is limited. Therefore, the models, though improved, still face challenges in consistently predicting song popularity accurately.

<p>
  <img align="center" width="600" alt="Each result of GBR in Cross-validation" src="https://github.com/user-attachments/assets/7c98576a-c958-45ff-a5e5-2cc8efaf3e12">
  <p> </p>
  <img align="center" width="600" alt="Each result of RF Regression in Cross-validation" src="https://github.com/user-attachments/assets/e09608c1-0fea-45d0-a93e-9cc85d9b7561">
</p>

Hyperparameter tuning slightly enhanced model performance by optimising key parameters. For the GBR model, the optimal parameters were a tree depth of 2, 90 models, and a learning rate of 0.1 (Table 1). For the RF Regression model, the best parameters were a tree depth of 6, 150 models, and a node size of 10 (Table 2).

<table align="center">
    <thead>
        <tr>
            <th>Tree Depth</th>
            <th>Number of Models</th>
            <th>Learning Rate</th>
        </tr>
    </thead>
    <tbody align="right">
        <tr>
            <td>2</td>
            <td>90</td>
            <td>0.1</td>
        </tr>
    </tbody>
</table>
<p align="center"><b><i>Table 1: Best Parameter for GBR</b></i></p>


<table align="center">
  <thead>
    <tr>
      <th>Tree Depth</th>
      <th>Numner of Models</th>
      <th>Node Size</th>
    </tr>
  </thead>
  <tbody align="right">
    <tr>
      <td>6</td>
      <td>150</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
<p align="center"><b><i>Table 2: Best Parameter for RF</b></i></p>

Implementing these parameters resulted in slight improvements in both models. For the RF model, the Mean Squared Error (MSE) decreased from 125.59 to 123.283, and the R-squared (R²) value increased from 0.161 to 0.176, indicating enhanced accuracy and reduced prediction error. The GBR model exhibited more significant improvement, with the MSE dropping from 137.663 to 129.017 and the R² value rising from 0.08 to 0.138. These enhancements suggest that while both models benefited from hyperparameter tuning, GBR showed a more notable increase in performance.

Despite these improvements, both models still exhibited relatively low predictive performance, highlighting the challenges in accurately predicting song popularity. The cross-validation results showed that although individual folds had low MSEs, the overall predictive performance across all folds was more robust and generalised, reflected by higher average MSE and lower R² values. This shows that the models' generalisability is still limited, even though they can function effectively on certain data subsets. Improved predicted accuracy and resilience may require additional feature discovery and refining, as well as other modelling methods.

<table align="center">
  <thead>
    <tr>
      <th></th>
      <th>Default Parameters</th>
      <th>Optimized Parameters</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="left">R-square</td>
      <td align="right">0.161</td>
      <td align="right">0.176</td>
    </tr>
    <tr>
      <td align="left">MSE</td>
      <td align="right">125.509</td>
      <td align="right">123.283</td>
    </tr>
    <tr>
      <td align="left">RMSE</td>
      <td align="right">11.203</td>
      <td align="right">11.103</td>
    </tr>
  </tbody>
</table>
<p align="center"><b><i>Table 3: Random Forest Regression Results</b></i></p>

<table align="center">
  <thead>
    <tr>
      <th></th>
      <th>Default Parameters</th>
      <th>Optimized Parameters</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="left">R-square</td>
      <td align="right">0.08</td>
      <td align="right">0.138</td>
    </tr>
    <tr>
      <td align="left">MSE</td>
      <td align="right">137.663</td>
      <td align="right">129.017</td>
    </tr>
    <tr>
      <td align="left">RMSE</td>
      <td align="right">11.733</td>
      <td align="right">11.359</td>
    </tr>
  </tbody>
</table>
<p align="center"><b><i>Table 4: Gradient Boosting Regression Results</b></i></p>

The frequency of splits at each tree level in the Random Forest model is used to determine the importance of a feature. The findings (Table 5) show that, when split across all tree levels, the "year" of release is the most reliable indicator of song popularity. Other important features are "danceability" and "valence," which are also commonly used for splits at different levels, highlighting their crucial role in forecasting song popularity. These results highlight how each feature affects the model's predictive power differently, providing insightful information for improving model performance and guiding data interpretation.

<table align="center">
  <thead>
    <tr>
      <th>Features</th>
      <th>splits (level 0)</th>
      <th>splits (level 1)</th>
      <th>splits (level 2)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="left">year</td>
      <td align="right">38</td>
      <td align="right">49</td>
      <td align="right">65</td>
    </tr>
    <tr>
      <td align="left">valence</td>
      <td align="right">18</td>
      <td align="right">37</td>
      <td align="right">40</td>
    </tr>
    <tr>
      <td align="left">danceability</td>
      <td align="right">17</td>
      <td align="right">31</td>
      <td align="right">48</td>
    </tr>
        <tr>
      <td align="left">dB</td>
      <td align="right">16</td>
      <td align="right">24</td>
      <td align="right">41</td>
    </tr>
        <tr>
      <td align="left">bpm</td>
      <td align="right">15</td>
      <td align="right">25</td>
      <td align="right">43</td>
    </tr>
        <tr>
      <td align="left">energy</td>
      <td align="right">15</td>
      <td align="right">31</td>
      <td align="right">58</td>
    </tr>
        <tr>
      <td align="left">liveness</td>
      <td align="right">15</td>
      <td align="right">20</td>
      <td align="right">38</td>
    </tr>
        <tr>
      <td align="left">duration</td>
      <td align="right">12</td>
      <td align="right">24</td>
      <td align="right">45</td>
    </tr>
        <tr>
      <td align="left">acousticness</td>
      <td align="right">3</td>
      <td align="right">18</td>
      <td align="right">28</td>
    </tr>
        <tr>
      <td align="left">speechiness</td>
      <td align="right">1</td>
      <td align="right">10</td>
      <td align="right">22</td>
    </tr>
  </tbody>
</table>
<p align="center"><b><i>Table 5: Attribute Statistics – Random Forest Regression</b></i></p>

<br >

## Conclusion
The findings show that although RF and GBR model performance is improved by hyperparameter adjustment, total predicted accuracy is still quite poor.  "year," "valence," and "danceability" were identified by the analysis as the three main factors that determine song popularity. The relatively low R2 values, however, imply that song popularity may be strongly influenced by other factors that have not yet been investigated. To increase forecast accuracy, future work should concentrate on adding more features and experimenting with other modelling strategies. This study emphasises how difficult it is to forecast song popularity and how important it is to keep improving models.




