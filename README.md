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

### New Features
The features we used in our final model include 
#### Quantitative Features:
- minutes
- n_steps
- calories
- n_ingredients

#### Ordinal Features:
#### Nominal Features:
'minutes','review','description','n_steps','calories','n_ingredients'

### Hyperparameters
For Hyperparameters we used Polynomial Features to try to see if our data had any nonlinear relationship. To test the best degree for our data, we tried running polynomial regression by transforming our quantitative columns using PolynomialFeatures to d degrees from range(1,26). However, we found that our data has the lowest RMSE when using degree of 1 (0.5754801669400889) while all other degrees had a higher degree(~ 0.7120073200102263). This shows that our original model using linear regression of degree 1 was using the optimal hyper parameters. In addition we also used Grid Search CV for our decision tree model. We used it for hyperparameters of max_depth, min_sample_split, and criterion. We found that the best hyperparameters for our decision tree w/o text columns were {'criterion': 'gini', 'max_depth': 2, 'min_samples_split': 2}.

### Improvement
In the beginning we altered our baseline model by including different features ie. 'minutes','review','description','n_steps','calories','n_ingredients'. We chose to use review and description because we believed that they would contain the data that would most accurately correlate to the rating category. We transformed these columns into quantitative columns using tdif vectorizer. We also transformed minutes and calories into quantiles. In additon we believed that other categories were important (n_steps,n_ingredients) as they could have an effect on the rating of a recipe ie. longer steps may lead to lower rating or more ingredients may lead to better taste, higher score. This linear regression model with transformed columns had R^2 for training and testing of (0.3595132779525668, 0.3383757209722451) and a RMSE of (0.5698228214585664, 0.5741282072255443). We then experimented with polynommial regression but found that linear regression ie. d = 1 was the best hyper parameter for polynomial regression using for loop to find the best degree. Furthermore we also utilized a decision tree with the optimal hyperparameters however for the decision tree we weren't able to use the text columns review and description. For our decision tree we found that the accuract for the training and testing data of(0.7736046285492026,0.7727397035497456). We didn't use RMSE to score our decision tree model as RMSE is often not a good scoring method for multi class classifiers. In addition, we also used precision to score our decision tree and found that the precision score was 0.5971266494421488. Finally we used a Random Forest classifier with the same columns as our original model (linear regression with transformed models). This model had the best accuract by far for both training and testing of (0.9998359101516919, 0.7799777571149884). In addition the precision score of this model was 0.730321601552345 which was much higher than our decision tree. In conclision we decided to pick Random Forest Classifier because it had the highest accuracy and precision score compared to all other models.

### Confusion Matrix Visualization
![not](\Users\dakam\Desktop\p5\Recipe-Ratings-Prediction-Model\assets\download.png)

## Fairness Analysis

Since the median cooking time in minutes is 35 minutes, we split our two groups into recipes with a cooking time over 103 minutes, and recipes with a cooking time under 35 minutes.

#### **Group X:** Recipes with cooking time under 35 minutes

#### **Group Y:** Recipes with cooking time over 35 minutes

Since we chose to use a regression model, our evaluation metrics will be RMSE.

### **Null Hypothesis:** 
Our model is fair. Its RMSE for recipes with cooking time under and over 35 minutes are roughly the same, and any differences are due to random chance.

### **Alternative Hypothesis:**
Our model is unfair. Its RMSE for recipes with cooking time under 35 is lower than its RMSE for recipes with cooking time over 35 minutes. 

For our permutation test, we are examining if the distribution of RMSE when using the model on Group X and Group Y come from the same distribution. Since the two distributions are quantitative numerical, and have similar basic shapes, our test statistic is going to be the difference in RMSE.

### Conclusion