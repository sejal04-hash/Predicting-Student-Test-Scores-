# Predicting-Student-Test-Scores-
Predicting Student Test Scores — Kaggle Playground Series S6E1

Competition Overview

Predicting Student Test Scores is a Kaggle Playground Series competition (Season 6, Episode 1). The objective is to predict the continuous exam_score target from student-related features.

Task: Regression

Target: exam_score

Metric: Root Mean Squared Error (RMSE)

Train rows: 630,000

Test rows: 270,000

Status: Competition completed

Kaggle: https://www.kaggle.com/competitions/playground-series-s6e1

Kaggle describes the dataset as synthetically generated for a beginner-friendly machine-learning challenge.

My Result

Final submission:

submission_ensemble.csv

Metric

Score

Final Score

8.72951

Public Score

8.70242

Dataset

Numerical Features

age

study_hours

class_attendance

sleep_hours

Categorical Features

gender

course

internet_access

sleep_quality

study_method

facility_rating

exam_difficulty

Identifier

id

The id column was treated as an identifier and was not used as a predictive feature.

Approach

The project focused on learning ensemble learning for tabular regression.

1. Preprocessing

The workflow included:

Separate exam_score from the features.

Remove id from model features.

Check missing and invalid values.

Handle missing categorical values.

Handle missing numerical values.

Encode categorical variables where required.

Keep train/test preprocessing consistent.

2. Base Models

Three boosting models were used:

LightGBM

XGBoost

CatBoost

These models were selected to provide different learning behaviour for tabular data.

3. 5-Fold Cross Validation

A shuffled 5-fold K-Fold strategy was used.

Dataset
   |
   +-- Fold 1 -> Validation
   +-- Fold 2 -> Validation
   +-- Fold 3 -> Validation
   +-- Fold 4 -> Validation
   +-- Fold 5 -> Validation

Each row received an out-of-fold prediction from a model that did not train on that row.

4. Weighted Blending

Predictions from the three base models were combined.

Initial blend:

LightGBM  -> 40%
XGBoost   -> 35%
CatBoost  -> 25%

Conceptually:

Final Prediction =
    0.40 × LightGBM
  + 0.35 × XGBoost
  + 0.25 × CatBoost

5. Ridge Stacking

OOF predictions from the base models were also used as inputs to a Ridge regression meta-model.

LightGBM ──┐
XGBoost  ──┼──> Ridge Meta-Model ──> Final Prediction
CatBoost ──┘

This allowed the meta-model to learn how to combine the base predictions.

OOF Predictions

Out-of-Fold (OOF) predictions were important for stacking.

For each training row, its OOF prediction came from a model that had not seen that row during training. This makes the predictions more suitable as training data for the meta-model.

Evaluation Metric

Kaggle evaluates submissions using Root Mean Squared Error (RMSE):

RMSE = sqrt(mean((actual - predicted)^2))

Lower RMSE indicates smaller prediction errors.

Submission

The required submission format was:

id,exam_score
630000,97.5
630001,89.2
630002,85.5

The final submission contained 270,000 predictions, matching the competition test set.

Key Learning Outcomes

This competition helped practice:

Regression

RMSE

Tabular data preprocessing

Categorical feature handling

LightGBM

XGBoost

CatBoost

K-Fold Cross Validation

Out-of-Fold predictions

Weighted blending

Stacking

Ridge meta-models

Kaggle submission validation

Main Lesson

Ensemble learning is not simply about adding more models. A useful ensemble combines models whose prediction errors are sufficiently different so that one model can compensate for another.

Possible Future Improvements

Potential experiments include:

Feature engineering

Better categorical encoding

Hyperparameter tuning

More diverse base models

Neural networks for tabular data

Optimizing blend weights

More advanced stacking

Careful pseudo-labeling experiments

Residual/error analysis

Any improvement should first be checked with cross-validation instead of relying only on the public leaderboard.

Resources

Kaggle Competition: https://www.kaggle.com/competitions/playground-series-s6e1

Kaggle Data: https://www.kaggle.com/competitions/playground-series-s6e1/data

Kaggle Leaderboard: https://www.kaggle.com/competitions/playground-series-s6e1/leaderboard

Author

Sejal Raykhere

B.Tech CSE — Artificial Intelligence & Machine Learning

Focus areas:

Machine Learning

Data Science

Computer Vision

Python

Backend Development

AI/ML Projects

Project Summary

Built a regression ensemble for the Kaggle Playground Series S6E1 Student Test Scores competition using LightGBM, XGBoost, CatBoost, K-Fold cross-validation, weighted blending, and Ridge stacking.

Final Kaggle Score: 8.72951
