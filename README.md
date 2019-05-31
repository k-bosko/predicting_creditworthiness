## Table of Contents

1. [Installation](#Installation)
2. [Description](#Description)
3. [Data](#Data)
4. [File Descriptions](#File-Descriptions)
5. [Results](#Results)
6. [Acknowledgements](#Acknowledgements)

## Installation
- Python 3.7.2
- Libraries: 
  - [NumPy](http://www.numpy.org/)
  - [Pandas](http://pandas.pydata.org)
  - [matplotlib](http://matplotlib.org/)
  - [scikit-learn](http://scikit-learn.org/stable/)

You will also need to have software installed to run and execute an [iPython Notebook](http://ipython.org/notebook.html)

## Description

The business problem was formulated as follows:
> You work for a small bank and are responsible for determining if customers are creditworthy to give a loan to. 
> Your team typically gets 200 loan applications per week and approves them by hand. 
> Due to a financial scandal that hit a competitive bank last week, you suddenly have an influx of new people applying 
> for loans for your bank instead of the other bank in your city. All of a sudden you have nearly 500 loan applications 
> to process this week! Your manager sees this new influx as a great opportunity and wants you to figure out 
> how to process all of these loan applications within one week.

## Data 
`credit-data-training.xlsx` - credit approvals from the past loan applicants the bank has ever completed.

`customers-to-score.xlsx` - the new set of customers to be processed


## File Descriptions

You can find the results of the analysis in either html form or complete Jupyter Notebook:

* [Predicting_Creditworthiness.html](https://github.com/k-bosko/predicting_creditworthiness/blob/master/Predicting_Creditworthiness.html)
* [Predicting_Creditworthiness.ipynb](https://github.com/k-bosko/predicting_creditworthiness/blob/master/Predicting_Creditworthiness.ipynb)

Alterinatively, run one the following commands in a terminal after navigating to the top-level project directory `predicting_creditworthiness/` (that contains this README):

```bash
ipython notebook Predicting_Creditworthiness.ipynb
```  
or
```bash
jupyter notebook Predicting_Creditworthiness.ipynb
```

This will open the iPython Notebook software and project file in your browser.

## Results

To identify the creditworthy applicants, I performed the following steps:

- **Step 1: Preprocessing**
  - removed certain predictors either due to low variability or no logical connection with the target
  - imputed missing values with median
  - one-hot encoded the predictors and the target with `pd.get_dummies()`
  - split the data into training and testing sets with `train_test_split()` 

- **Step 2: Creating a Training and Predicting Pipeline**
  - initialized and fit classification models:
    - `DecisionTreeClassifier()`
    - `RandomForestClassifier()`
    - `AdaBoostClassifier()`
  - created `predict_evaluate()` function to predict `X_test` values 
  - evaluated the performance of the three models via `accuracy_score()`, `f1_score()`, `roc_curve()`
  
- **Step 3: Improving Results**
  - performed a grid search optimization via `GridSearchCV(`) for two parameters `n_estimators` and `learning_rate`
  - made predictions using the unoptimized and optimized model
  - compared the before-and-after scores (accuracy and F-score) on the testing data
  
- **Step 4: Predicting the Creditworthiness**
  - performed the same data transformations on new loan applicants data as was done on the training set
  - predicted the creditwothiness using the optimized `RandomForestClassifier()`
  
- **Step 5: Extracting Feature Importance**
  - determined the top5 most predictive features using `feature_importances_` attribute


## Acknowledgements

Having started learning Python, I decided to rewrite the project I first completed in [Alteryx](https://www.alteryx.com)
within the [Predictive Analytics for Business Nanodegree at Udacity](https://www.udacity.com/course/predictive-analytics-for-business-nanodegree--nd008).
