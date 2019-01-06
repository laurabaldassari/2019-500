# The `match1` Example

This is the place to find code for the `match1` example. We’ll use a small, simulated example to demonstrate some of the tools available in the Matching package. The data can be found in the match1.csv data file on the course website. 

The subjects are identified by ID #s in the `subject` variable (1-300), and we have 

- `exposure` status (78 “yes” and 222 “no”) as well as each subject’s 
- `age`, 
- sex, in the form of an indicator for `female`, 
- `race` (4 categories, labeled 1, 2, 3 and 4), 
- number of `comorbid` illnesses (out of a possible 9), 
- `serumK` (serum potassium level), 
- `wbc` (white blood cell count) and 
- a quantitative `outcome` (better results = higher outcome values).

We’re going to fit a logistic regression model to predict propensity for exposure on the basis of the main effects of six covariates: age, female, race (treated as a factor), comorbid (treated as a count), serumK, and wbc

Then, we’ll match exposed to unexposed patients using the Matching package, and look at [1] how effectively we balance the distributions of those covariates, and [2] obtain an average treatment effect on the treated (ATT) estimate for the causal effect of the exposure on outcome under each matching approach.

The matching approaches we’ll demonstrate are:

1.	1:1 matching on the propensity score, without replacement. [We’ll do this one in detail.]
2.	1:2 matching on the propensity score, without replacement.
3.	1:3 matching on the propensity score, without replacement.
4.	1:1 matching on the propensity score, with replacement.
5.	1:1 matching on the propensity score, with replacement, within groups defined by race.
6.	1:1 matching on the propensity score, with replacement, within a caliper
7.	Genetic matching, which automatically finds balance by using a genetic search algorithm to determine the optimal weight for each covariate within the matching algorithm.

All of this material is contained in [this PDF document](https://github.com/THOMASELOVE/500-2018/blob/master/data-and-code/match1/match1%20Description%202018.pdf). Sorry it's not in R Markdown.

