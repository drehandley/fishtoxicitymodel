# # Fish Toxicity Model

## Overview
The goal of this project was to build a linear regression 
model to predict the toxicity of chemicals to fish. I used 
the QSAR Fish Toxicity dataset from the UCI Machine Learning 
Repository which contains 908 chemicals and 6 chemical 
descriptors. My target variable was LC50 which measures 
the concentration of a chemical that kills 50% of fish 
in a test period of 96 hours.

## Dataset
The dataset came from the UCI Machine Learning Repository.
It contained 908 rows and 7 columns. The dataset had no 
column headers and used semicolons as separators which 
I had to handle when loading the data.

The 6 features are:
- CIC0: information index of the chemical structure
- SM1_Dz: 2D matrix descriptor
- GATS1i: measures how atoms interact with each other
- NdsCH: counts a specific type of carbon atom
- NdssC: counts another type of carbon atom
- MLOGP: measures how well the chemical dissolves 
  in water vs fat

Target Variable:
- LC50: how toxic the chemical is to fish
  lower value means more toxic
  higher value means less toxic



## Process

### Step 1 - Exploring the Data (explore.ipynb)
I started by exploring the raw dataset to understand 
what I was working with. I checked for missing values, 
data types, distributions and correlations. Some things 
I found during EDA:
- The dataset had no missing values
- All columns were already numerical so no 
  encoding was needed
- MLOGP had the strongest correlation with LC50 at 0.65
- SM1_Dz and GATS1i had moderate correlations with LC50
- NdsCH and NdssC had weak correlations with LC50
- No multicollinearity was detected between features
- The Z Score method detected some outliers that 
  needed to be handled in the cleaning phase

### Step 2 - Cleaning the Data (clean.ipynb)
Based on what I found during EDA I cleaned the dataset.
Since there were no missing values I focused mainly on 
handling outliers. I used the Z Score method to remove 
any rows where a value was more than 3 standard 
deviations from the mean.
- Original dataset: 908 rows
- Cleaned dataset: fewer rows after outlier removal
- The cleaned dataset was saved as clean_fish_toxicity.csv

### Step 3 - Building the Model (model.ipynb)
I built a baseline linear regression model using the 
cleaned dataset. I split the data into 80% training 
and 20% testing and scaled the features using 
StandardScaler before training the model.

Model Results:
- R2 Score: 0.4501
- RMSE: 1.0029

The R2 score of 0.45 means my model explains 45% of 
the variation in LC50. The RMSE of 1.0029 means on 
average my predictions are off by about 1 LC50 unit. 
For a baseline linear regression model these results 
are reasonable.

## What I Learned
This was my first machine learning project and I learned 
a lot throughout the process. I learned how important 
it is to explore and clean your data before building 
a model. I also learned that a simple linear regression 
model might not always capture the full relationship 
between features and the target variable.

## Further Research
If I were to continue working on this project I would:
- Try more advanced models like Ridge and Lasso regression
- Collect more data to improve model performance