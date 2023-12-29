# Predicting Recipe Ratings Model 
### Aadhya Naveen (anaveen@ucsd.edu) 

## Introduction

### Question: Do recipes with higher average ratings tend to have lower levels of total fat?

Welcome! The dataset I have chosen illustrates recipes and various information like steps, categories, and ratings of each recipe. The data is pulled from a website called food.com, and as humans we know the importance of food in our day-to-day lives therefore, this analysis will provide insight on these recipes :)

The data is broken down into 2 csv files: RAW_recipes.csv and RAW_interactions.csv. I merged both of the dataset with the common column 'id' which refers to the unique recipe id. Once I merged the datasets, the number of rows in the dataset were 234,429.

As for my research question - I was curious on whether the ratings had any relationship with the total fat content of each recipe. Therefore my question is ** Do recipes with higher average ratings tend to have lower levels of total fat? **

Here's a breakdown on some of the important columns in the dataset.
'name': name of the recipe

'id': unique id of recipe

'nutrition': gives nutritional content of the recipe in the form of a list [calories, total fat, sugar, sodium, protein, saturated fat, carbs] [NOTE] for this particular analysis, we will be looking at the total fat content of each recipe!

'ratings': ratings for each recipe

---
## Cleaning and Exploratory Data Analysis

### Data Cleaning

(1) The data is broken down into 2 csv files: RAW_recipes.csv and RAW_interactions.csv. I merged both of the dataset with the common column 'id' which refers to the unique recipe id. Once I merged the datasets, the number of rows in the dataset were 234,429.

(2) Replaced all zeros with np.nan - This indicates that the values are actually missing instead of of low amount. For example, when we replace the 0 for np.nan in the ratings columns, it indicates that the value is actually missing instead of the recipe getting a low rating.

(3) Created a series called 'avg_rating' based of the ratings columns - which instead took the average rating of each recipe since there were duplicates in the dataset. Then did a merge to add this column to the dataset.

(4) Dropped columns like 'user_id', 'recipe_id', 'date', 'contributor_id', 'review' and 'submitted', 'steps', and 'tags' because I did not need them in the analysis that I was doing and they were taking up too much space. 

(5) In the nutrition column - it appears that each entry is a list when it is actually a string! Therefore, using the eval function I looped through each of the enteries and turned them into lists. Then, since the second element of the list refers to the total_fat, created a new column 'total_fat' which only has the fat portion of the nutrition list.

(6) Just to keep numbers clean and to make them easier to work with, I rounded the floats in 'total_fat' and 'average_rating' to 2 decimal places. This is so that runtime is faster and it would be easier to work with. 

| name                                |     id |   minutes | tags                                                                                                                                                                                                                        | nutrition                                    |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |   rating |   average_rating |   total_fat |
|:-------------------------------------|-------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|-----------------:|------------:|
| 1 brownies in the world    best ever | 333281 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |        4 |                4 |          10 |
| 1 in canada chocolate chip cookies   | 453467 |        45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |        5 |                5 |          46 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |                5 |          20 |

### Pivot Tables, Aggregate Statistics

|   rating |   total_fat |
|---------:|------------:|
|        1 |     37.0564 |
|        2 |     32.7669 |
|        3 |     31.6405 |
|        4 |     29.9404 |
|        5 |     31.7924 |

This is a pivot tabel that shows the mean total_fat for each rating in general. I used this because it is easier to look at since the cateogories for ratings are broader versus average_rating which has sperates the rating by .1 which is hard to find trends with. As we can see in the pivot table, there seems to be a slight decrease in fat as ratings increase. The mean total fat is about 37 for when the rating is 1 star, versus the total fat being about 32 when the rating is 5. But considering the distribution of ratings, it could be that since there are less observations with lower ratings the means tend to be higher. 

|   rating |   total_fat |
|---------:|------------:|
|        1 |          19 |
|        2 |          20 |
|        3 |          20 |
|        4 |          19 |
|        5 |          20 |

This pivot table focuses on the identical columns but examines the median instead of the mean. Considering that the mean can be significantly impacted by outliers and distribution patterns, analyzing the median offers an alternative viewpoint on the distribution of the "total_fat" column concerning ratings.

## Assesment of Missingness

### NMAR analysis
I think that the description column of the dataset is NMAR. It could be that users leave the description for a recipe as blank because they feel that adding a description takes too much time and they may feel that it is redundant. To make the description column as MAR and to see if it depends on external observations, we can see if the addition of a time taken to fill out the review survey is added to see if users are truly rushing to write their reviews and tend to skip out on the description because they feel that it takes to much time and because their recipe is self-explanatory.

### Missingness Dependency

Test #1
Null Hypothesis (H0): The distribution of "n_steps" when the description is missing is identical to the distribution of "n_steps" when the description is not missing.

Alternative Hypothesis (Alt Hyp): The distributions of "n_steps" are different between cases where the description is missing and cases where it is not.

Observed Statistic: The difference in means between the two groups.

Rationale: If there is a higher number of steps, it suggests that the description is more likely to be left blank. This is because detailed steps may make the inclusion of a description less necessary, leading to a potential difference in the distribution of "n_steps" between cases where the description is present and cases where it is missing.
<iframe src="assets/steps.html" width=800 height=600 frameBorder=0></iframe>
We then use a permuatation test to shuffle the n_steps columns 500 times.
<iframe src="assets/dist.html" width=800 height=600 frameBorder=0></iframe>
The observed statistic is 0.71 and p-value is 0.0 because the distribution is so far from the observed statistic. This means we reject the null, and accept the null hypothesis. Missingness of description is MAR because description is dependent on n_steps. We reject null hypothesis that description is not dependent on n_steps. 

## Hypothesis Testing
H0: Average Ratings and total fat have no relationship, ratings are evenly distributed among different levels of fat 

H1: Recipes with average higher ratings tend to have lower levels of fat

Differences in means - Test Statistic 

Significance level - 0.05

Observed Pvalue: 3.22

Pvalue: 0.0

Reject null hypothesis that the two groups come from the same distriibution, but cannot conclude that high rating causes lower fat.

## Problem Identification & Introduction
Uses the "recipes ratings" data from Project 3 which has been cleaned for this model. The datasets were merged, missing values were handled with being replaced with zero to avoid errors with pipelines since nan is incompatible, and columns were renamed for better comprehension. The full Exploratory Data Analysis can be available here for more information [Project 3](https://aadhyanav.github.io/Recipe_Ratings/). 

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

### New Features

I added a new column called "bad_review" which specifically catches the words "awful" "bad" and "zero" in the review - indicating negative review which could help predict whether an recipe is considered to be successful or not. As for the 2 new transformations, in addition to the previous pipeline I did a quantile transformation on n_steps and standardized the n_ingredients column. 

<iframe src="assets/log.html" width=800 height=600 frameBorder=0></iframe>

As for n_steps, since I logged it right before doing the quantile transformation, the logged distribution looks like the image above. The reason I felt that doing a quantile transformation would be best is because quantile transformations are less sensitive to outliers and since the numbers are logged which means that the variance is not constant - this would help normalize the distribution more than the normal z-score transformation. 

<iframe src="assets/ingredients.html" width=800 height=600 frameBorder=0></iframe>

For ingredients, I felt that standardizing the values would be the best transformation because the distribution is heavily skewed to the left and has a long tail. 

I initially tried using Binarizer() on my newly made bad_review column, but realised that the pipeline intereprets boolean numbers into integers and that Binarizer() is more helpful for columns with more categories. Honestly, given the dataset I felt I was pretty limited over what other columns I could add into my pipeline considering how there were colums like 'id', 'name', 'steps' that were pretty unrelated with recipe ratings. 

### Modeling Algorithm, Hyperparameters, and Performance
I used a RandomForestClassifaction because of how well it works with datasets that are unbalanced. As for the CVsearch grid in finding the best possible parameters for my model, the process took a really long time in my jupyter notebook. The best performance parameters ended up having a max depth of 120 and 50 estimators for the random forests. It seems like the model becomes more accurate with the more depth that is added, but for runtime purposes the largest depth parameter that I tested was 120. After the all the feature engineering and Grid Search, my f-1 score became 78 percent, which increased 2 percent from the baseline performace. Perhaps if I had added more variables the performance could have gone better, but I think that majority of the improvement came from tuning the hyperparameters. 

## Fairness Analysis

The question that I have picked is: Does my model perform worse for recipes that have more than 8 ingredients versus recipes that have less than 8 ingredients?
- Null Hypothesis: The model is fair, and the accuracy is the same for both groups: groups with more than 8 ingredients versus groups with less than 8 ingredients
- Alternative Hypothesis: The model is not fair, the accuracy is higher for groups with more than 8 ingredients.
- Test statistic: Difference in accuracy scores
- Significance level: 0.05

### Conclusion
According to my findings, the permutation p-value is 1.0, which indicates that the null hypothesis should be rejected. Even though the p-value givens a strong indication to reject the null, we cannot be too sure about accepting the alternative hypothesis. Therefore there's a high possibility that the model is not fair and the accuracy score is indeed higher for groups with more than 8 ingredients. 



