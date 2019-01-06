# Homework 2 for 500 (Due 2019-02-07)

## Submission Details

Submit your work via [Canvas](https://canvas.case.edu/) before noon on 2019-02-07. 

## 1. Create a sample.

Create a sample of 1000 subjects from the `dig1.csv` data describing the DIG study. Specify a random seed (via `set.seed`) to select your sample of 1000 subjects. Ensure that your sample does not include any subject who has missing information on the indicator of previous myocardial infarction, `PREVMI`. (You may want to identify such subjects in advance and filter them out of the dig1 data before you sample.)

## 2. Create a Table 1.

The Table 1 should describe the data according to whether or not the subject had a previous myocardial infarction (`PREVMI`) across each of these 12 variables. 

Variable | Description
-------: | -----------------------------------------------------
`TRTMT` | Treatment group (1 = DIG, 0 = Placebo)
`AGE` | Age in years
`RACE` | White (1) or Non-White (2)
`SEX` | Male (1) or Female (2)
`EJF_PER` | Ejection Fraction (percent)
`CHESTX` | Chest X-ray (CT ratio)
`BMI` | Body-Mass Index
`KLEVEL` | Serum Potassium level (mEq/l)
`CREAT` | Serum Creatinine level (mg/dl)
`CHFDUR` | Approximate Duration of CHF (mos.)
`EXERTDYS` | Dyspnea on exertion (see note)
`FUNCTCLS` | Current NYHA Functional Class (1 = I, 2 = II, 3 = III, 4 = IV)

Note that the `dyspnea` categories are: 0 = None or Unknown, 1 = Present, 2 = Past, 3 = Present and Past

Be sure to correctly represent each of the categorical variables as factors, rather than in the numerical form they start in. Label your factors to ease the work for the viewer, and reduce or eliminate the need to look at a codebook. Also, be sure to accurately report whether any missing values are observed in this sample.

*Note*: You're going to have to do this again with a revised sample in step 4, so it's worth it to code this in a reproducible way.

## 3. Build a logistic regression model.

Build a logistic regression model for previous MI using the main effects of the 12 variables above. I'd call the model `m1` that predicts the log odds of previous myocardial infarction (`PREVMI`) on the basis of the main effects of each of the twelve variables in your table above, for your sample of 1000 subjects. How many observations does your model actually fit results for? (This is asking for the number of subjects without any missingness, across all variables in your model.)

## 4. Redefine your sample and rebuild the Table and Model.

Assuming you have at least one missing value in a predictor in your model for question 3, re-define your sample to include only the observations which are "complete cases" with no missingness on any of the key variables we're looking at. Specify the number of subjects (< 1000) that remain in your new sample. 

Now, **redo both Tasks 2 and 3** to describe this new sample and use it to fit a model. Call the new model `m2`. Verify that no missingness plagues this new model. 

## 5. Add the fitted probabilities from Question 4 to your data, then plot them against observed status.

Use the model (`m2`) you built in Task 4 to add the fitted probability of previous myocardial infarction to your sample used to create `m2`. Produce an attractive and useful graphical summary of the distribution of fitted probabilities of previous myocardial infarction broken down into two categories by the patient's actual `PREVMI` status in this sample. I suggest rounding the probabilities to two decimal places before graphing.

