# Second-Hand-Car-Price-Prediction

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

library(readr) -> For importing data into the environment

library(dplyr) -> For data manipulation

library(ggplot2) -> To provide visualizations

library(summarytools) -> For summary statistics

library(patchwork) -> To make plot composition in R extremely simple and powerful

library(paletteer) -> A collection of various color palettes found in different R packages.

library(tidymodels) -> For fitting models

## Data Preparation and Cleaning

-Imported the cars csv file into the environment

-Selected 12 features excluding CAR_ID from the total of 13 features in the file.

-Transformed Fuel_Type, Owner_Type, Transmission and Year features from Character to factor features


