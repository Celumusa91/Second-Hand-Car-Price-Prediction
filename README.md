# Second-Hand-Car-Price-Prediction

![](Cars_image.png)

## Project Overview

The task is to develop a machine learning model that can predict the selling price of a car based on its specifications. This predictive model will assist potential buyers and sellers in estimating the fair market value of a car.

## Data Sourcing

The csv cars dataset was downloaded from kaggle website. Its contains the following features;

**Car_ID**: A unique identifier for each car listing.

**Brand**: The brand or manufacturer of the car (e.g., Toyota, Honda, Ford, etc.).

**Model**: The model of the car (e.g., Camry, Civic, Mustang, etc.).

**Year**: The manufacturing year of the car.

**Kilometers_Driven**: The total kilometers driven by the car.

**Fuel_Type**: The type of fuel used by the car (e.g., Petrol, Diesel, Electric, etc.).

**Transmission**: The transmission type of the car (e.g., Manual, Automatic).

**Owner_Type**: The number of previous owners of the car (e.g., First, Second, Third).

**Mileage**: The fuel efficiency of the car in kilometers per liter.

**Engine**: The engine capacity of the car in CC (Cubic Centimeters).

**Power**: The maximum power output of the car in bhp (Brake Horsepower).

**Seats**: The number of seats available in the car.

**Price**: The selling price of the car in INR (Indian Rupees), which is the target variable to predict.

## Packages/ Tools employed

All data cleaning steps and analysis were done inside R-studio using R-markdown format. The following packages were used for the analysis;

- library(readr) -> For importing data into the environment

- library(dplyr) -> For data manipulation

- library(ggplot2) -> To provide visualizations

- library(summarytools) -> For summary statistics

- library(patchwork) -> To make plot composition in R extremely simple and powerful

- library(paletteer) -> A collection of various color palettes found in different R packages.

- library(tidymodels) -> For fitting models

## **Data Preparation and Cleaning**

- Imported the cars csv file into the environment

- Selected 12 features excluding CAR_ID from the total of 13 features in the file.

- Transformed Fuel_Type, Owner_Type, Transmission and Year features from Character to factor features


## **Exploratory Data Analysis**

### **STEP 1** Feature Distributions

- Distribution of Dependent variable (Price) to see if there are any outliers.

- Distribution of numeric features with measures of central tendency

- Pivote numeric features to a longer format and Visual numeric features distribution

- Distribution of categorical features

- Pivote categorical features to a longer format and visualize distribution

### **STEP 2** Checking Relationships

This step checks if there is statistical correlations between the Price being predicted and the Predictor features

- Price and numeric features

- Price and categorical features

### **STEP 3** Selecting sample features statistically correlate with Price

The Price, Engine, Power, Mileage, Year, Transmission, Owner_Type,
Fuel_Type, Brand and Model variables were selected to make up the sample of variables predict price. These  variables are variables that were discovered to correlate with Price.

## **Create a data splitting formula**

This step uses the initial_split function from the resamples package from tidymodels to split the data into the training and validation sets.
The **training** function create the training set and the **testing** function creates the  test set. 80% of the sample data is allocated to the train set while the remaining 20% is allocated to the testing set.

# Let's fit a linear model to predict Price

## Create a linear model specification

Set the model engine to **"lm"** and the model mode to **"regression"**

## Fit the linear model specification

Use the **fit** function to fit the model on the train_sample (training set)

## Evaluate the model perfomance by predicting with the test_sample data set

Create **lm_results** which shows actual price alongside the predicted price values obtained from the model.

## Calculate linear model evaluation metrics

- rmse - The root mean squerd error is the average difference between values predicted by a model and the actual values.

- rsq - The R-squared value that measures the proportion of the variance in the dependent variable explained by the independent variables in the model.

# In search for a better model (rmse, rsq), Let's fit the linear model using resapmles (10-folds cross validation)

## Create data preprocessing recipe

- **step_dummy()** - Encodes categorical features to numeric forms.

- **step_nzv()** - Step near-zero variance create a specification of a recipe that will potentially remove variables that are highl sparse and unbalanced.

- **step_normalize()** - Scales and normalizes numeric variables to prevent features with large values to from producing coefficients that disproportionately affect the predictions.

- **step corr()** - Create a specification that remove numeric independent varaibles that are highly correlated with each other.


## Bundle the lm model specification and the preprocessing recipe into a workflow

Use the **workflow()** funtion from tidymodels library

## Create a 10-folds cross validation

First set the seed so that the split to ensure reproducible results of the folds.

## Fit the linear model workflow with resamples

Use the **fit_resamples()** function.

## Evaluate the cross validation model

- Use **collect_predictions()** functions to provide the model predicted values of price.

- Use **collect_metrics()** functions to provide the rmse and the rsq values of the model.


# Let’s look for a better model (fit xgbbost model)

## Create a xgboost model specification

Set the model engine to **"xgboost"** and the model mode to **"regression"**. Set trees, tree_depth and the learn rate to tune() for the model to estimate best hyperparameter values that suite the data.

## Data preprocessing recipe for xgboost model

- Step_dummy()

- Ste_normalize()

## Bundle the xgboost specification and the recipe into a workflow

Bundle the xgboost model Specification and the xgboost recipe into a **xgboost_workflow** using the **workflow()** function.

## Create xgboost parameter grid

Create a tree_grid for the specified xgboost hyperparameters. Levels is set equals 5 which means 5 combinations of each hyperperameter which will enable 125 models to be fitted and then select the our best comination model.

## Tune the xgboost model workflow

Use the tune_grid function and the sample folds(10-folds cross-validation) and use the **show_best()** function to show the model best combination with the lowest rmse and rsq values
Use the **select_best()** function to select our best model that we can use later to predict Price with new dataset. 

To see analysis report check()

## Best tree

Use the select_best function to extract the best tree model with the lowest rmse. About 1 500 trees, a tree depth of 4 and a learning rate of 0.0825 give a low rmse of 173091. This rmse states that our model is off by 173091 when predicting Car Price.

# **Results**

Our first linear model gave us a rmse of **400035** and a rsq of **0.888**. Fitting with resamples gave us an improved rmse **282040** and rsq of **0.866**. Our xgboost model gave us a far better **173091** value of rmse. This means that xgboost model best predict price using our selected variables.
