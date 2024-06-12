# Relationship between Number of Ingredients and Calories of Recipes
Authors: Shruti Yamala and Arshia Vadhani

# Overview
We are analyzing the relationship between the number of ingredients of a given recipe and the calories of that given recipe.

# Introduction
For this project, we utilized the Recipes and Ratings Data Frame. We found that it would be easiest to draw practical conclusions from this data frame and that our deliverable could aid in making everyday decisions. Especially during the summertime, when people find more free time to cook and experiment with more things, the findings of our project will give them the tools and insight to help them choose the right recipes to replicate. Our project is centered around using other factors to predict the number of calories that a recipe will output. Our data frame contains 234,429 rows and below you will find the most relevant columns we worked with.
<img width="896" alt="Screen Shot 2024-06-10 at 5 20 40 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/adf180f6-bc5d-4be0-8e7c-15090b52f68e">
<img width="908" alt="Screen Shot 2024-06-11 at 4 43 04 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/9addc141-e1c7-4c83-8299-b61a7b0d99cd">

# Data Cleaning and Exploratory Data Analysis

We began to clean our data by merging the two data frames we were originally given, recipes and interactions. With this merge on recipe_id, we were able to create one large recipes_and_ratings data frame that contained the contents of the recipe, the minutes taken to make it, the number of steps, the nutrition information, the number of ingredients, etc. Not knowing what direction we wanted to go in, we created extra columns that we believed could give us some insight into the relationship between the recipe and its contents. The added columns in particular that were most helpful were "Calories": this column extracted the number of calories from the nutrition information columns, "Average Rating": this column helped us find the average rating per recipe as given by people who have made them or (the user_ID).

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
## Missingness Dependency

### Missingness of Rating on Cooking Time

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

### Missingness of Rating on Number of Ingredients

<iframe
  src="assets/missing2a.html"
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

Our goal for our prediction problem was to utilize the columns in the data frame to be able to predict the number of calories an ingredient would have given the other information(the presence of high-calorie ingredients, cuisine, other nutrition information, etc.). We chose to build a regression model with there response variable being the number of calories. We chose this response variable as it is necessary information  that most people tend to take into consideration when choosing a recipe. Our metric for evaluating our model was the RMSE because of the error magniitude sensitivity. RMSE punishes larger deviations to the true calorie at disproportionaltely larger rate. This is good as the aim for our prediction model is to get as accurate of a prediction as possible especially when tracking nutrients and macros of meals. Further RMSE, has an easy interpretability allows us to compare the magnitude of the error in the same units as the predicted variables, so if our RMSE is 50, our predictions for calories are off by an average of 50 calories. 

# Baseline Model

# Final Model

# Fairness Analysis

Our fairness analysis consisted of:

Null: Our model was fair and prediction accuracy was the same for both groups, recipes with 7 or more ingredients and recipes with less than 7 ingredients. There was no significant difference between the RMSE’s for either group

Alternative: Our models prediction accuracy was unfair and its prediction accuracy for recipes with 7 or more ingredients was higher than recipes with less than 7 ingredients. 
The evaluation metric for models accuracy was the RMSE.

Our p-value threshold was again 0.05 for alpha. 
Our test statistic was difference in RMSE and we chose this because it would be easiest to directly compare how the model performed with more ingredients versus with less ingredients. It was a more straightforward comparison in prediction accuracy and we could draw a more concrete conclusion if we were able to see how well the model perfomed across both groups.
As a final result, our observed difference between the group was about 40 calories and the p-value was 0.31, which was above the threshold of 0.05 and therefore we can fail to reject the null hypothesis, indicating that our model is pretty fair and draws constant conclusions across both groups no matter if recipes are categorized as high ingredient or low ingredient recipes. ”
