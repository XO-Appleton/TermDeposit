# Term Market Deposit

## Problem Statement

Given the banking information of customers, predict if they would subscribe to a term deposit. Also, identify the potential subscribers from the existing records.

## Data Description

The data comes from the direct marketing efforts of a European banking institution. The marketing campaign involves making a phone call to a customer, often multiple times to ensure a product subscription, in this case, a term deposit. Term deposits are usually short-term deposits with maturities ranging from one month to a few years. The customer must understand when buying a term deposit that they can withdraw their funds only after the term ends. All customer information that might reveal personal information is removed due to privacy concerns.

age : age of customer (numeric)

job : type of job (categorical)

marital : marital status (categorical)

education (categorical)

default: has credit in default? (binary)

balance: average yearly balance, in euros (numeric)

housing: has a housing loan? (binary)

loan: has a personal loan? (binary)

contact: contact communication type (categorical)

day: last contact day of the month (numeric)

month: last contact month of the year (categorical)

duration: last contact duration, in seconds (numeric)

campaign: number of contacts performed during this campaign and for this client (numeric, includes the last contact)

y - has the client subscribed to a term deposit? (binary)

## Approach

The dataset is mixed of numerical and categorical features, so we first processed the categorical features and mapped them into numerical feature vectors using one-hot encoding. 

The dataset is highly imbalanced with 92.76% of the client not subscribing to a term deposit and only 7.24% of them did. So we upsampled the minority class and downsampled the majority class.

We then tested a variety of models including Logistic Regression, SVC, Random Forest, KNN, Ada Boost, and XGBoost.

## Metrics

Since the dataset is highly imbalanced, accuracy would not be a good metric. So we instead use the F1 score to evaluate the models.

## Final Model

The final model chosen was the tuned XGBClassifier(n_estimators=50, max_depths=6,random_state=22). It was trained on the resampled balanced training set and achieved  94% training accuracy and 92% testing accuracy and an f1-score of 0.53 for class 1 on the test set. Its performance was found to be most optimized with a probability threshold of 0.6.

Final model result:

![final model result](https://github.com/XO-Appleton/TermDeposit/assets/41369365/afb01942-0ead-4eb8-9ba4-1d0a68329613)

## Summary

The main challenge of the project is the imbalanced dataset which was mitigated by a mix of upsampling, downsampling, and choosing F1 score over accuracy for evaluation.

After converting the categorical features to numerical ones, there were 24 features in total, using backward feature selection, we were able to narrow it down to the top 5 most important features:

Converted Feature Importances:

![converted_feature importance](https://github.com/XO-Appleton/TermDeposit/assets/41369365/ca09b548-3797-44a8-989e-1eb8fd4a8a68)

Using fewer features, the accuracy dropped by 2% and the f1 score dropped from 0.53 to 0.52, but it significantly simplified the model.

Five-feature model result:

![five feature model result](https://github.com/XO-Appleton/TermDeposit/assets/41369365/2cea179f-6fa3-4491-9e8f-948c34d6e590)

Using the model to predict the original dataset, we found 1670 false positives, that is, clients not subscribed to a term deposit but the model predicte
d them to be subscribed. Therefore, we consider these clients potential subscribers to the term deposit.

