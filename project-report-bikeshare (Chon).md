# Report: Predict Bike Sharing Demand with AutoGluon Solution
Chon Sek Lai

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?

Thanks to the hint in the project template provided by Udacity, students are prompted to replace negative values with zero; hence, Kaggle does not accepts negative values.

### What was the top ranked model that performed?

Among my 3 submissions, WeightedEnsemble_L3 was ranked highest for 2 times and WeightedEnsemble_L2 was ranked highest for 1 time. These powerful WeightedEnsemble models are what make AutoGluon stand out among all machine learning algorithms available.

The AWS Machine Learning Team has carefully designed the bagging and stacking processes behind these WeightedEnsembles (which at the same time use XGBoost and CatBoost, among all other models, as its weak learners) to make AutoGluon almost unbeatable.


## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?

A few things stand out from EDA:
  1. data are evenly distributed across the four seasons
  2. holidays and weekends are recorded, which allow the model to differentiate pattern of weekdays from that of weekends/holidays
  3. rentals from non-registered casual users are significant (marketing department may want to do something about it)
  4. weather conditions such as temperature, humidity, windspeed are all well recorded, which can help with building more accurate model

Datetime contains useful information (in a condensed manner) such as Time, Day of Week, and Month which can potentially help the model make more accurate predictions. It is indeed a good idea to decompress Datetime and convert it into 3 extra columns.


### How much better did your model preform after adding additional features and why do you think that is?

After adding additional features (e.g. hour, Day of Week, and Month), model accuracy has improved significantly (with Kaggle score changing from 1.78841 to 0.74169).

The explicit information of time, Day of Week, and Month (instead of the compressed Datetime) allows the model to pick up patterns within the data more easily.


## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?

The model did not improve much after trying different values of hyper parameters (with Kaggle score changing from 0.74169 to 0.57669); this is in line with  Alex Smola's (VP of AWS Machine Learning Team) opinion (that hyper-parameters tuning is a bit overhyped, at least with the advent of AutoGluon).


### If you were given more time with this dataset, where do you think you would spend more time?

I would say trying to find extra features to improve the model, because all the predictive power of the features in existing data has also been extracted by AutoGluon.

One suggestion would be to record the locations of where a bike was picked up as well as where a bike was returned, since certain locations can matter more under certain weather conditions.


### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.

|model       |timelimit|num_leaves in XGBoost|tree_dept in CatBoost|learning_rate in XGBoost|learning_rate in CatBoost|Kaggle Score|
|initial     |   600   |      default        |      default        |      default           |       default           |   1.78841  |
|add_features|   600   |      default        |      default        |      default           |       default           |   0.74169  |
|hpo         |   900   | between 100 and 400 |   between 4 and 12  |  between 0.01 and 0.1  |   between 0.01 and 0.1  |   0.57669  |


### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](https://superchon-udacity.s3.us-west-1.amazonaws.com/AutoGluon_model_train_score_BikeShare_Kaggle.png)


### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](https://superchon-udacity.s3.us-west-1.amazonaws.com/AutoGluon_model_test_score_BikeShare_Kaggle.png)


## Summary

This is a great project where students can:
- practise EDA
- read AutoGluon documentation for hyper-tuning
- have a deeper understanding of the Kaggle platform
- become more familiar with AWS in general

This project also allows students to compare two different approaches for improving the model's prediction accuracy. It turns out that finding additional features should always be explored, because there is only so much that hyper-parameter tuning can do.
