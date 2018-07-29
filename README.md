# New York City Taxi Fare Prediction

This repository contains the submission notebook for the Kaggle competition [New York City Taxi Fare Prediction](https://www.kaggle.com/c/new-york-city-taxi-fare-prediction) from Google Cloud. The objective was to get some familiarity with the [XGBoost](https://xgboost.readthedocs.io/en/latest/index.html) library in Python.

## Submission results

- 22/178 with a RMSE score of 3.44303 on the public leaderboard (29/07/2018)

## What I have learned

1) XGBoost consists of an ensemble of trees but, unlike random forests, the trees used in XGBoost are weak learners (not fully grown trees). This method works by reducing bias by the aggregation of trees to the ensemble, since individual weak learners have high bias but low variance. Unlike random forests, this method is sequential and cannot be so easily parallelized.

2) This dataset has lots of outliers and erroneous data that must be cleaned:
  - Rows with negative values for the fare amount,
  - Rows with values for the pick up and drop off coordinates far away from NYC.
  - Rows with a passenger count of up to 200.
  
## Future improvements

1) XGBoost has more hyperparameters to tune than random forests. We could try to improve results by tuning hyperparameters of the model using cross validation.

2) Converting the column 'pickup_datetime' to a datetime format to be able to extract information from this field has been found to be a bottleneck. This prevents us from using more data during training due to time constraints. 
