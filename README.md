# Predicting Recipe Ratings Model 
### Aadhya Naveen (anaveen@ucsd.edu) DSC80 Fall 2023

## Problem Identification & Introduction
Uses the "recipes ratings" data from Project 3 which has been cleaned for this model. The datasets were merged, missing values were handled with being replaced with np.nan instead of zero, and columns irelevant to the prediction were dropped from the dataset. 

This model predicts whether a recipe is “Satisfactory” or “Unsatisfactory” based on the data. It uses a classification prediction model using binary classification in which Satisfactory is 1 and Unsatisfactory is 0. The threshold for this binary classifcation is that any recipe with an average rating of 4.0 or higher was considered to be Satisfactory.
