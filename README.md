# New York City Taxi Fare Prediction

This repository contains the submission notebook for the Kaggle competition [New York City Taxi Fare Prediction](https://www.kaggle.com/c/new-york-city-taxi-fare-prediction) from Google Cloud. The objective was to get some familiarity with the [XGBoost](https://xgboost.readthedocs.io/en/latest/index.html) library in Python.

## Submission results

- 26/325 with a RMSE score of 3.03992 on the public leaderboard (05/08/2018)

## What I have learned

1) XGBoost consists of an ensemble of trees but, unlike random forests, the trees used in XGBoost are weak learners (not fully grown trees). This method works by 
reducing bias by the aggregation of trees to the ensemble, since individual weak learners have high bias but low variance. Unlike random forests, this method is 
sequential and cannot be so easily parallelized. The XGBoost implementation in Python does build each tree in parallel.

2) Hyperparameter tuning is quite important for performance. We have used cross-validation to tune the following parameters:
- max_depth: controls the maximum depth of each tree.
- subsample: controls the percentage of rows from the training dataset that are used when growing each tree. Subsampling occurs before each boosting iteration.
- colsample_bytree: controls the percentage of columns from the training dataset that are used when growing each tree. Subsampling occurs before each boosting iteration.
- eta: controls the step size shrinkage after each boosting step. 

3) This dataset has lots of outliers and erroneous data that must be cleaned:
  - Rows with negative values for the fare amount,
  - Rows with values for the pick up and drop off coordinates far away from NYC.
  - Rows with a passenger count of up to 200.
  
 4) Feature engineering was important to improve the performance of the model. According to the [NYC Taxi & Limousine Commission](http://www.nyc.gov/html/tlc/html/passenger/taxicab_rate.shtml) the following variables influence the value of the fare and were added to the dataset:
 - Distance from pickup to dropoff
 - Information on the date (day, hour, month, day of week, year)
 - Trips that start or end at an airport.
 
 5) Specifying the exact format to the to_datetime() function greatly helps in speeding up date conversion.
  
## Future improvements

- Scale the model to make use of more data, right now we use ~10% of the training dataset only. 
