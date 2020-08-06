# Sales Forecasting
As the name suggests, predicting future sales based on some parameters is **Sales Forecasting**.Why do we need to do it?,well
that depends on the company/user specific needs.We can do it to assess the following-:

1)To set targets
2)Make strategic Decisions
3)Prepare Operations

## About The Dataset
The dataset used is [Rossman-Store-Sales](https://www.kaggle.com/c/rossmann-store-sales) from kaggle. The aim was to forecast sales using the features
store,promotion, and competitor data.The submissions are to be evaluated on Root Mean Square Percentage Error(RMSPE).
![Formula](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/Screenshot%202020-08-06%20at%203.09.50%20PM.png)

## Exploratory Data Analysis
EDA performed [here.](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/EDA.ipynb)

## Modelling
First I have done some data preprocessing,which includes mappings and essential calculation,i've also applied **log transformation** to the target variable(Sales),
as in the [EDA](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/EDA.ipynb) we found out that the distribution of sales was a bit right skewed.What **log transformation**
does is that it'll take the log of all values  and try to normalize the data.For more info [click here](https://medium.com/@kyawsawhtoon/log-transformation-purpose-and-interpretation-9444b4b049c9).
The next step was fitting the model, which i did using **RandomForest**.
### RandomForest
Random forests are bagged decision tree models that split on a subset of features on each split.One advantage which i had using this model was, not a lot of pre-processing
had to be done , aslo the data didn't have to scaled/normalized.Random Forest works in the following way:-

**Original Dataset -> Randomized Bootstrap Copies -> Randomized Feature splits -> Ensemble Prediction**

The next step was looking at the feature importances,which is available as an attribute in the class.Then evaluation was done using the given evaluation metric and r2_score.

![](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/FeatureImportance.png)
## Hyperparamter-Tuning
In order to reduce the errors tuning the model needs to be done.
**Hyperparameters** are set manually before fitting the model to get the best model.I've used **RandomizedSearchCV**.


**RandomizedSearch** is a technique where random combinations of the hyperparameters are used to find the best solution for the built model.
The main advantage of **RandomizedSearchCV** is that randomized search and the grid search explore exactly the same space of parameters.
The result in parameter settings is quite similar, the run time for randomized search is drastically lower.

The parameters I used are n_estimators,max_depth,max_features,bootstrap and performed 3 fold cross validation.
![](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/Param.png)

We can see that the model underfits when max depth<8 and overfits when max depth>9, so we can set max depth=9.Also their is a change in percentage error.

## Prediction
Finally Prediction on the test set is made using the model obtained after tuning and saved in [submission.](https://github.com/Aarsh2001/Rossmann-Sales/blob/master/Submission.csv)
