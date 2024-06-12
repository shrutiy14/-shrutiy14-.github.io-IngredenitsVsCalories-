# Relationship between Number of Ingredients and Calories of Recipes
Authors: Shruti Yamala and Arshia Vadhani

# Overview
We are analyzing the relationship between the number of ingredients of a given recipe and the calories of that given recipe.

# Introduction
For this project, we utilized the Recipes and Ratings Data Frame. We found that it would be easiest to draw practical conclusions from this data frame and that our deliverable could aid in making everyday decisions. Especially during the summertime, when people find more free time to cook and experiment with more things, the findings of our project will give them the tools and insight to help them choose the right recipes to replicate. Our project is centered around using other factors to predict the number of calories that a recipe will output. Our data frame contains 234,429 rows and below you will find the most relevant columns we worked with.
<img width="896" alt="Screen Shot 2024-06-10 at 5 20 40 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/adf180f6-bc5d-4be0-8e7c-15090b52f68e">
<img width="908" alt="Screen Shot 2024-06-11 at 4 43 04 PM" src="https://github.com/shrutiy14/-shrutiy14-.github.io-RecipeProject-/assets/129795184/9addc141-e1c7-4c83-8299-b61a7b0d99cd">

# Data Cleaning and Exploratory Data Analysis
We began to clean our data by merging the two data frames we were originally given, recipes and interactions. With this merge on recipe_id, we were able to create one large recipes_and_ratings data frame that contained the contents of the recipe, the minutes taken to make it, the number of steps, the nutrition information, the number of ingredients, etc. Not knowing what direction we wanted to go in, we created extra columns that we believed could give us some insight into the relationship between the recipe and its contents. The columns in particular that were most helpful were "Calories": this column extracted the number of calories from the nutrition information columns, "Average Rating": this column helped us find the average rating per recipe as given by people who have made them or (the user_ID) (KEEP WORKING HERE, EXPLAIN WHAT OTHER STEPS AND HOW IT AFFECTED OUR ANALYSIS)

## Cleaned Data Frame

| name | minutes | tags | nutrition | n_steps | ingredients | n_ingredients | user_id | recipe_id | date | rating | avg_rating | calories | nutrition_without_calories | total fat | sugar | sodium | protein | saturated fat | carbs | high_ing |
|------|---------|----------------|-----------|--------|--------------|-------|-------------|-------------|------------|----------|---------|------|--------|--------|-------|---------|---------|---------|----------|-------|
| 1 brownies in the world    best ever | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0] | 10 | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] | 9 | 386585.0 | 333281.0 | 2008-11-19 | 4.0 | 4.0 | 138.4 | [10.0, 50.0, 3.0, 3.0, 19.0, 6.0] | 10.0 | 50.0 | 3.0 | 3.0 | 19.0 | 6.0 | True |
| 1 in canada chocolate chip cookies | 45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings'] | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] | 12 | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips'] | 11 | 424680.0 | 453467.0 | 2012-01-26 | 5.0 | 5.0 | 595.1 | [46.0, 211.0, 22.0, 13.0, 51.0, 26.0] | 46.0 | 211.0 | 22.0 | 13.0 | 51.0 | 26.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 29782.0 | 306168.0 | 2008-12-31 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 1196280.0 | 306168.0 | 2009-04-13 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |
| 412 broccoli casserole | 40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli'] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 6 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions'] | 9 | 768828.0 | 306168.0 | 2013-08-02 | 5.0 | 5.0 | 194.8 | [20.0, 6.0, 32.0, 22.0, 36.0, 3.0] | 20.0 | 6.0 | 32.0 | 22.0 | 36.0 | 3.0 | True |

## Univariate Analysis
<iframe
  src="assets/univariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Bivariate Analysis
