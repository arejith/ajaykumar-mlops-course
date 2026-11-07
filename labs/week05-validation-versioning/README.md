# Week 05 Lab

Add validation checks to the Week 3-4 pipeline; version the dataset (DVC or equivalent).

Starter files for this week's lab will be added here before the lab session
(pulled into your repo via `git fetch upstream && git merge upstream/main`,
as introduced in the Week 1 lab).

## Of the two problems in the new batch, which would have been easier to miss if you were just skimming the data by eye? Why?
low values in annual income. Its sill numeric and non - negetive. 

## Your first annual_income check (min_value=0) technically ran and technically passed on the corrupted data. What made it the wrong check anyway?
The min check of annual income 0 would mean that the person would require more checks, beacause there is high chance for the data to be corrupted. outlier and unconventional data should be double checked for the accuracy of the model in solving real world challenges

## How does today's validation suite relate to Week 3's data contracts -- is a Great Expectations suite the contract itself, or something else?
no great expectation is not a contract. it turns the reuqirements into checks before training and validating the model. Data contract would be expectations that the consumer and producer agrees on, it defines the ownership of the data as well.
## When you rolled back with DVC, what did Git actually track versus what did DVC manage? Why split it that way?
Git tracks the code and .dvc file
sample .dvc file 
```bash
outs:
- md5: d73aef4b3c2238999bd9d8dda56abb2a
  size: 20206
  hash: md5
  path: loan_applications.csv

```
DVC tracks the actual dataset.
 During rollback, Git restored the v1 pointer, and dvc checkout restored the CSV version identified by that pointer.

 We split them because the dataset can be very large and cannot be stored in git. so git contains data version while that can be restored to restore the data locally 

## Before today, an MLflow run could tell you the hyperparameters and accuracy behind a model but not the data version. What does logging data_hash actually let you answer that you couldn't before?

The hash identifies the data version. whether the dataset had changed or not.

