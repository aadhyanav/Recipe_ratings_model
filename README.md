# Predicting Recipe Ratings Model 
### Aadhya Naveen (anaveen@ucsd.edu) DSC80 Fall 2023

## Problem Identification & Introduction
Uses the "recipes ratings" data from Project 3 which has been cleaned for this model. The datasets were merged, missing values were handled with being replaced with np.nan instead of zero, and columns irelevant to the prediction were dropped from the dataset. The full Exploratory Data Analysis can be available here [Project 3](https://aadhyanav.github.io/Recipe_Ratings/). 

This model predicts whether a recipe is “Satisfactory” or “Unsatisfactory” based on the data. It uses a **classification** prediction model using **binary classification** in which Satisfactory is 1 and Unsatisfactory is 0. The threshold for this binary classifcation is that any recipe with an average rating of 4.5 or higher is considered to be Satisfactory. Therefore, the **response variable will be "Recipe Satisfaction"** which is a binary measure of whether the recipe had an average rating or 4.5 or higher. The reason I chose this as the response variable was because the column 'average rating' had values that ranged from 0 to 5 which was hard to classify, therefore I was able to make clear categories for the column by setting a threshold that determined the satisfaction of each recipe. For the metrics that I will be using to evaluate the model, I will be using the F-1 score over accuracy because of the imbalance among the distribution when the response variable is plotted. At the time of the prediction, all information will be known. 

<iframe src="assets/ratings.html" width=800 height=600 frameBorder=0></iframe>
As the distribution shows, there is a massive imbalance between "Satisfactory" (1) and "Unsatisfactory" (0) - which indicates that using the F-1 score would be more plausible in this situation. 

## Baseline Model

This model intends to predict whether a recipe will turn out to be sastifactory or unsatisfactory.

Here are some of the features we will be testing this model upon:

- **Quantitative Features**: n_steps, n-ingredients 
- **Response Variable** Recipe Satisfaction (which is omitted from the features)
- **Categorical Variable** tags (nominal since there is no ranking/hierachy among the different tags)

Therefore, that leaves us with the only categorical variable, which is tags. I will be one hot encoding this column to quantify this column so that it can be used as a feature. It creates every unique tag as a seperate column which can be included in the predictive model. For the other transformations, since there are no more categorical variables to do transformations on, I will be doing a log transformation on the n_steps column because it the data is skewed to the right. The log transformation is good for reducing distributions that are skewed to the right.

Before using a RandomForestClassifer to run the pipelines through, I made sure to limit the tree depth to reduce runtime. The model had an F-1 score of 76 percent, which is reasonably good, but can definetly be improved upon. Considering how this model only uses 3 of the original columns from the dataset, to increase the performance more data can be added that ensures satisfaction. 

## Final Model
I added a new column called "bad_review" which specifically catches the words "awful" "bad" and "zero" in the review - indicating negative review which could help predict whether an recipe is considered to be successful or not. As for the 2 new transformations, in addition to the previous pipeline I did a quantile transformation on n_steps and standardized the n_ingredients column. I initially tried using Binarizer() on my newly made bad_review column, but realised that the pipeline intereprets boolean numbers into integers and that Binarizer() is more helpful for columns with more categories. 

I used a RandomForestClassifaction because of how well it works with datasets that are unbalanced. As for the CVsearch grid in finding the best possible parameters for my model, the process took a really long time in my jupyter notebook. Therefore, I felt that most likely the bigger parameters are better because more data can be fit inside - this a higher f-1 score due to more variation. 

## Fairness Analysis




