# Relationship between Number of Ingredients and Calories of Recipes
Authors: Shruti Yamala and Arshia Vadhani

# Overview
We are analyzing the relationship between the number of ingredients of a given recipe and the calories of that given recipe.

# Introduction
For this project, we utilized the Recipes and Ratings Data Frame. We found that it would be easiest to draw practical conclusions from this data frame and that our deliverable could aid in making everyday decisions. Especially during the summertime, when people find more free time to cook and experiment with more things, the findings of our project will give them the tools and insight to help them choose the right recipes to replicate. Our project is centered around using other factors to predict the number of calories that a recipe will output. Our data frame contains 234,429 rows and below you will find the most relevant columns we worked with.

<img width="896" alt="Screen Shot 2024-06-10 at 5 20 40 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/adf180f6-bc5d-4be0-8e7c-15090b52f68e">
<img width="908" alt="Screen Shot 2024-06-11 at 4 43 04 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/9addc141-e1c7-4c83-8299-b61a7b0d99cd">

# Data Cleaning and Exploratory Data Analysis

We began to clean our data by merging the two data frames we were originally given, recipes and interactions. 

1. Left merge the recipes and interactions datasets together. With this merge on recipe_id, we were able to create one large recipes_and_ratings data frame that contained the contents of the recipe, the minutes taken to make it, the number of steps, the nutrition information, the number of ingredients, etc. 

2. In the merged dataset, fill all ratings of 0 with np.nan. We believe this is because most rating systems range from 1-5, so a rating of 0 may not accurately reflect a user's true opinion of a certain recipe, so an input of 0 could be a data quality issue.

3. Find the average rating per recipe, as a Series.

4. Add this Series containing the average rating per recipe back to the recipes dataset

Not knowing what direction we wanted to go in, we created extra columns that we believed could give us some insight into the relationship between the recipe and its contents. The added columns in particular that were most helpful were "Calories": this column extracted the number of calories from the nutrition information columns, "Average Rating": this column helped us find the average rating per recipe as given by people who have made them or (the user_ID). Also, we extracted "total fat", "sugar", "sodium", "protein", "saturated fat", "carbs" from the "nutrition" column, allowing us to access each individual element of nutrition. We also created a column that is True for number of ingredients over 7 for a recipe, as we were interested in that concept for our bivariate analysis. 

Below are the columns of our cleaned df:

## Cleaned Data Frame

| name | minutes | tags | nutrition | n_steps | ingredients | n_ingredients | user_id | recipe_id | date | rating | avg_rating | calories | nutrition_without_calories | total fat | sugar | sodium | protein | saturated fat | carbs | high_ing |
|------|---------|----------------|-----------|--------|--------------|-------|-------------|-------------|------------|----------|---------|------|--------|--------|-------|---------|---------|---------|----------|-------|
| 1 brownies in the world    best ever | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0] | 10 | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] | 9 | 386585.0 | 333281.0 | 2008-11-19 | 4.0 | 4.0 | 138.4 | [10.0, 50.0, 3.0, 3.0, 19.0, 6.0] | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 | True |
| 1 in canada chocolate chip cookies | 45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings'] | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] | 12 | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips'] | 11 | 424680.0 | 453467.0 | 2012-01-26 | 5.0 | 5.0 | 595.1 | [46.0, 211.0, 22.0, 13.0, 51.0, 26.0] | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 29782.0 | 306168.0 | 2008-12-31 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 1196280.0 | 306168.0 | 2009-04-13 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 768828.0 | 306168.0 | 2013-08-02 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |

## Univariate Analysis

For our univariate analysis, we looked into the distribution of calories amongst recipes within our data frame. The present trend is that a large majority of all recipes lie within the 0-2500 calorie range.
<iframe
  src="assets/univariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Bivariate Analysis

For our bivariate analysis, we explored the relationship between the proportion of all calories in each subgroup, high-numbered ingredient recipes (7+), and low-numbered ingredient analysis (<7). We found that recipes labeled high-ingredient contain a higher proportion of the overall calories as compared to recipes that are low-ingredient.

<iframe
  src="assets/bivariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Interesting Aggregates

We wanted to further understand rhe relationship between number of ingredients and calories. The pivot table below shows the mean, sum, minimum, and maximum calories of recipes grouped by the number of ingredients. We see a very general increase in mean calories as the number of ingredients rises, but it is important to note that the pivot table also showcases that a few simpler recipes with fewer ingredients tend to have higher mean calorie values, suggesting that high-calorie ingredients are often used in simpler recipes. 


|   n_ingredients |   ('mean', 'calories') |   ('sum', 'calories') |   ('min', 'calories') |   ('max', 'calories') |
|----------------:|-----------------------:|----------------------:|----------------------:|----------------------:|
|               1 |               1151.86  |      110578           |                   7.8 |                3590.2 |
|               2 |                395.96  |      924962           |                   0   |               12135.5 |
|               3 |                283.122 |           2.0263e+06  |                   0   |               13101.5 |
|               4 |                305.826 |           3.90234e+06 |                   0   |               45609   |
|               5 |                331.232 |           6.70712e+06 |                   0   |               17551.6 |
|               6 |                357.845 |           7.5355e+06  |                   0   |               17554   |
|               7 |                393.29  |           9.59864e+06 |                   0.7 |                8300.5 |
|               8 |                383.002 |           9.78686e+06 |                   1   |                9702.6 |
|               9 |                416.447 |           1.02929e+07 |                   0.3 |               17280.4 |
|              10 |                435.213 |           9.29921e+06 |                   0.7 |               18268.7 |
|              11 |                468.779 |           8.82852e+06 |                   2.8 |               18656   |
|              12 |                464.954 |           6.9413e+06  |                   0.3 |               21497.8 |
|              13 |                484.344 |           5.94532e+06 |                   1.5 |               15309.6 |
|              14 |                514.04  |           4.32564e+06 |                   2   |               11036.6 |
|              15 |                552.521 |           3.55437e+06 |                   4.8 |               22371.2 |
|              16 |                609.078 |           2.7981e+06  |                  19.2 |               28930.2 |
|              17 |                554.704 |           1.66689e+06 |                   2.5 |               13029.1 |
|              18 |                617.204 |           1.21898e+06 |                  12.3 |                5329   |
|              19 |                585.077 |      711453           |                  40.2 |                9131.8 |
|              20 |                662.043 |      697132           |                  24.4 |                6551.1 |
|              21 |                778.759 |      438441           |                  60.7 |                6827.9 |
|              22 |                701.687 |      434344           |                  38.6 |               10952.1 |
|              23 |                660.945 |      206876           |                 133.2 |                9456.2 |
|              24 |                591.681 |      104136           |                 135.7 |                3753.1 |
|              25 |                766.61  |       45996.6         |                  79.6 |                1885.9 |
|              26 |                840.441 |       84044.1         |                 169.6 |                3267.5 |
|              27 |               1301.2   |       58553.8         |                  77.2 |               26604.4 |
|              28 |                670.14  |       28816           |                 139.9 |                1519.7 |
|              29 |                880.897 |       27307.8         |                 274.1 |                3756.6 |
|              30 |                678.464 |       22389.3         |                 248.6 |                1390.2 |
|              31 |                872.454 |       11341.9         |                 203.4 |                1760.2 |
|              32 |                864.475 |        3457.9         |                 363.1 |                1031.6 |
|              33 |                338.2   |         338.2         |                 338.2 |                 338.2 |
|              37 |              10687.7   |       10687.7         |               10687.7 |               10687.7 |


# Assessment of Missingness

## NMAR Analysis

Review, rating, and description were three columns of the merged dataframe that had missing values. We believe that the missingness of the "review" column is NMAR because the missingness likely depends on the column itself; considering factors like user satisfaction (strong vs not strong opinions of the recipes), user engagement with the review platform (if they are someone who often leave reviews vs not), and even technical difficulties or time restrictions could have prevented the users from leaving a review.

## Missingness Dependency

To analyze if the missingness of the "rating" column was MAR on some other column of the dataframe, we proceeded to conduct a few hypothesis tests, both with a significance level of 0.05 and test statistic of the absolute difference in means.

### Missingness of Rating on Cooking Time

Null Hypothesis: The missingness of the "rating" column does not depend on cooking time (minutes).

Alternative Hypothesis: The missingness of the "rating" column does depend on cooking time (minutes).

Running a permutation test 500 repetitions, we achieved a p-value of 0.134, which is higher than our significance level; we fail to reject the null. So, the missingness of the "rating" column likely does not depend on the cooking time of the recipe. 

<iframe
  src="assets/missing1a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/missing1b.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

So, what other columns could the missingness of "rating" potentially depend on?

### Missingness of Rating on Number of Ingredients

Null Hypothesis: The missingness of the "rating" column does not depend on number of ingredients.

Alternative Hypothesis: The missingness of the "rating" column does depend on number of ingredients.

Running a permutation test 500 repetitions, we achieved a p-value of 0.0, which is lower than our significance level; we reject the null in favor of the alternative hypothesis. So, the missingness of the "rating" column likely does  depend on the number of ingredients in the recipe. Note the significant distance the observed test statistic is from the empirical distribution: it is understandable why the p-value was 0.0.

<iframe
  src="assets/missingAgain.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/missing2b.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing

For our hypothesis test, we formed our null hypothesis as

Null: Recipes with 7 or more ingredients will have the same calorie counts as those under 7.

Alternative: Recipes with 7 or more ingredients will have a greater calorie count as those with under 7. 

The simulation we used was a permutation test and this was because we wanted to compare if our two distributions appeared to come from the same population. We hypothesized that recipes with more ingredients would contains a larger number of calories simply due to the increase in volume of what went into the recipe. We set our significance level to 0.05 and chose difference in group means as our test statistic. The significance level of 0.05 is standard and difference in group means made it easy to interpret the overall difference in between the distribution of our two numerical variables. We ran the permutation test by creating two separate categories for each group called “high_ing” where recipes were given a True or False based on the “n_ingredient” column. We then shuffled “high_ing” 500 times. The result of our hypothesis test was an observed difference of 119.29092982758556 and a p-value of 0.0 which is less than our threshold meaning we reject the null hypothesis. This would make some sense as we can see a trend implied between recipes deemed “high-ingredient” and a larger proportion of the calories within our bivariate distribution. 

<img width="908" alt="Screen Shot 2024-06-12 at 1 04 41 AM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/73f42952-9c0d-47d3-827d-056316c6a4a8">


# Framing a Prediction Problem

Our goal for our prediction problem was to utilize the columns in the data frame to be able to predict the number of calories an ingredient would have given the other information(the presence of high-calorie ingredients, cuisine, other nutrition information, etc.), which is a REGRESSION problem because we are predicting a numerical outcome. 

We chose to build a regression model with the response variable being the number of calories. We chose this response variable as it is necessary information that most people tend to take into consideration when choosing a recipe. The information known at the "time of prediction" are all the columns available to us in the cleaned dataset, except the calories column which we are trying to predict.

Our metric for evaluating our model was the RMSE because of the error magniitude sensitivity. RMSE punishes larger deviations to the true calorie at disproportionaltely larger rate. This is good as the aim for our prediction model is to get as accurate of a prediction as possible especially when tracking nutrients and macros of meals. Further RMSE, has an easy interpretability allows us to compare the magnitude of the error in the same units as the predicted variables, so if our RMSE is 50, our predictions for calories are off by an average of 50 calories. 

# Baseline Model

We utilized a linear regression model utilizing the n_ingredients and n_steps features in our recipes_ratings_df, both quantitiative. We decided to go with Linear Regression for our baseline because it is simple, but effective to begin the process of model building for this regression problem. We split our dataframe into training and testing sets, utilizing a 80-20 split, because we want our model have the foundation of our training data without overfitting to the training data.

Our baseline model had an RMSE of about 588.5. Here are some physical statistics, comparing 5 indexes from the predicted calories (y_pred) and true calories (y_test).


|        |   predicted_cals |
|-------:|-----------------:|
|  44111 |          383.901 |
| 107113 |          393.064 |
|  46961 |          450.821 |
| 130647 |          367.583 |
| 134708 |          431.569 |

|        |   true_cals |
|-------:|------------:|
|  44111 |       306.9 |
| 107113 |        97.7 |
|  46961 |       643.5 |
| 130647 |       275.1 |
| 134708 |       394.9 |


# Final Model

As our RMSE for our baseline model was fairly large, we wanted to improve this considerably in our final model. 

## Adding Features

1. Ingredient encoding by creating binary features of specific ingredients (known to be high-calorie): butter, sugar, oil, cheese, cream. 
2. Cuisine type by creating binary features to identify whether the cuisine is Mexican. We tried many different variations of identifying cuisines, but identifying whether a recipe was Mexican or not proved to have the better results.
3. We included total fat, sugar, sodium, protein, saturated fat, and carbs features extracted from the original "nutrition" column, all features that can indirectly affect the calorie content of a recipe. 
4. Of course, we included the numerical features from our baseline as well, n_steps and n_ingredients.

## Modeling Algorithm

We ended up choosing the Lasso Regression model, which is a form of regularization for linear models. Regularization helps address the mistakes caused when we tend to overfit on the training data. Measuring the level of regularization strength, alpha, was the hyperparameter we chose to tune so we could avoid the issue of overfitting our training data!

For finding the best hyperparameter for alpha, out of 'lasso__alpha': [0.001, 0.01, 0.1, 1, 10], we performed Grid Search Cross Validation with 5 folds. The best hyperparamater proved to be 0.1. 

The final model's RMSE was 37.7. Since this was a clear increase from my baseline model, the final model considerably improved predicting calories than the baseline.

# Fairness Analysis

Our fairness analysis consisted of:

Null: Our model was fair and prediction accuracy was the same for both groups, recipes with 7 or more ingredients and recipes with less than 7 ingredients. There was no significant difference between the RMSE’s for either group

Alternative: Our models prediction accuracy was unfair and its prediction accuracy for recipes with 7 or more ingredients was higher than recipes with less than 7 ingredients. 
The evaluation metric for models accuracy was the RMSE.

Our p-value threshold was again 0.05 for alpha. 

Our test statistic was difference in RMSE and we chose this because it would be easiest to directly compare how the model performed with more ingredients versus with less ingredients. It was a more straightforward comparison in prediction accuracy and we could draw a more concrete conclusion if we were able to see how well the model perfomed across both groups.
As a final result, our observed difference between the group was about 21 calories and the p-value was 0.71, which was above the threshold of 0.05 and therefore we can fail to reject the null hypothesis, indicating that our model is pretty fair and draws constant conclusions across both groups no matter if recipes are categorized as high ingredient or low ingredient recipes. ”
