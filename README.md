# Predicting Recipe Ratings Model 
### Aadhya Naveen (anaveen@ucsd.edu) DSC80 Fall 2023

## Problem Identification & Introduction
Uses the "recipes ratings" data from Project 3 which has been cleaned for this model. The datasets were merged, missing values were handled with being replaced with np.nan instead of zero, and columns irelevant to the prediction were dropped from the dataset. The full Exploratory Data Analysis can be available here [Project 3](https://aadhyanav.github.io/Recipe_Ratings/). 

This model predicts whether a recipe is “Satisfactory” or “Unsatisfactory” based on the data. It uses a **classification** prediction model using **binary classification** in which Satisfactory is 1 and Unsatisfactory is 0. The threshold for this binary classifcation is that any recipe with an average rating of 4.5 or higher is considered to be Satisfactory. Therefore, the **response variable will be "Recipe Satisfaction"** which is a binary measure of whether the recipe had an average rating or 4.5 or higher. For the metrics that I will be using to evaluate the model, I will be using the F-1 score over accuracy because of the imbalance among the distribution when the response variable is plotted. 

<iframe src="assets/ratings.html" width=800 height=600 frameBorder=0></iframe>
As the distribution shows, there is a massive imbalance between "Satisfactory" (1) and "Unsatisfactory" (0) - which indicates that using the F-1 score would be more plausible in this situation. 

## Baseline Model

This model intends to predict whether a recipe will turn out to be sastifactory or unsatisfactory.

Here are some of the features we will be testing this model upon:

**Quantitative Features**: minutes, n_steps, n-ingredients, average_rating
**Response Variable** Recipe Satisfaction (which is omitted from the features)
Therefore, that leaves us with the only categorical variable, which is tags. I will be one hot encoding this column to quantify this column so that it can be used as a feature. For the other transformations, since there are no more categorical variables to do transformations on, I will be standardizing the minutes feature since the distribution is heavily skewed to the right. 


