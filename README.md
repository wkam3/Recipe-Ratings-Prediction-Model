# Recipe-Ratings-Prediction-Model
#### by William Kam and Gina Roberg
## Framing the Problem
---
### Prediction Problem: Predict Ratings of Recipes

In order to predict the **ratings** of recipes, we are building a **regressor model** and extracting features from the data of the reviews given to the recipes.  We chose the rating column because we wanted to see the relationship between different features extracted from reviews and how people perceive(rate) the recipes.   The metric we are going to use to evaluate our model is **RMSE**. We are going to use RMSE because it measures the average root squared difference between the predicted and actual recipe ratings, while penalizing larger errors more than smaller ones.  It is suitable for this regression model because the goal is to minimize the error between the predicted values and the actual values.

## Baseline Model
---

For our baseline model, we are using many of the columns created from the nutrition column as features, specifically total fat, sugar, sodium, protein, saturated fat, carbohydrates, as well as minutes.  All of our features were quantitative. The features for total fat, sugar, sodium, protein, saturated fat, and carbohydrates were all extracted from the nutrition column, which we performed in our data cleaning from our EDA.

#### Quantitative Features:
- total fat 
- sugar
- sodium
- protein
- saturated fat
- carbohydrates
- minutes

Using these features the performance of our model is not as good as it could be, being that the RMSE is greater than 1.

## Final Model
State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process.

Describe the model you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance.

Optional: Include a visualization that describes your model’s performance, e.g. a confusion matrix, if applicable.

## Fairness Analysis

Since the median cooking time in minutes is 35 minutes, we split our two groups into recipes with a cooking time over 103 minutes, and recipes with a cooking time under 35 minutes.

#### Group X: Recipes with cooking time under 35 minutes

#### Group Y: Recipes with cooking time over 35 minutes

Since we chose to use a regression model, our evaluation metrics will be RMSE.

### Null Hypothesis: 
Our model is fair. Its RMSE for recipes with cooking time under and over 35 minutes are roughly the same, and any differences are due to random chance.

### Alternative Hypothesis: 
Our model is unfair. Its RMSE for recipes with cooking time under 35 is lower than its RMSE for recipes with cooking time over 35 minutes. 

For our permutation test, we are examining if the distribution of RMSE when using the model on Group X and Group Y come from the same distribution. Since the two distributions are quantitative numerical, and have similar basic shapes, our test statistic is going to be the difference in RMSE.

### Conclusion