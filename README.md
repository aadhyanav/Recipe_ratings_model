# Predicting Recipe Ratings Model 
### Aadhya Naveen (anaveen@ucsd.edu) DSC80 Fall 2023

## Problem Identification & Introduction
Uses the "recipes ratings" data from Project 3 which has been cleaned for this model. The datasets were merged, missing values were handled with being replaced with np.nan instead of zero, and columns irelevant to the prediction were dropped from the dataset. The full Exploratory Data Analysis can be available here [Project 3](https://aadhyanav.github.io/Recipe_Ratings/).

This model predicts whether a recipe is “Satisfactory” or “Unsatisfactory” based on the data. It uses a **classification** prediction model using **binary classification** in which Satisfactory is 1 and Unsatisfactory is 0. The threshold for this binary classifcation is that any recipe with an average rating of 4.0 or higher is considered to be Satisfactory. Therefore, the **response variable will be "Recipe Satisfaction"** which is a binary measure of whether the recipe had an average rating or 4.0 or higher. 

