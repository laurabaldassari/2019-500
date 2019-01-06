# Homework 3 for 500 (Due 2019-03-07)

## Submission Details

Submit your work via [Canvas](https://canvas.case.edu/) before noon on 2019-03-07.

- I recommend a close look at [the toy example](https://github.com/THOMASELOVE/500-2018/tree/master/data-and-code/toy_example) and other examples from our [Data and Code page](https://github.com/THOMASELOVE/500-2018/tree/master/data-and-code).

## Data

We have completed the data collection in a simulated study of 400 subjects with cancer, where 150 have received an intervention, while the remaining 250 received usual care control. The primary aims of the study are to learn about the impact of the intervention on patient survival and whether or not the patient enters hospice. The `canc3.csv` data file is available above.

### The Codebook

The data file includes 400 observations, on 12 variables.

Variable | Description | Notes
----------: | -----------------| --------------------------------------------------------------------------------
`subject` | Study ID number  | 1-250 are control, 251-400 are intervention
`treated` | Treatment status | 1 = intervention (150), 0 = control (250)
`age`     | Patient age      | At study entry, Observed range: 34, 93 years
`female`  | Patient sex      | 1 = female (n = 258), 0 = male (n = 142)
`race`    | Patient's race   | 1 = Caucasian / White (n = 317), 0 = not (n = 83)
`married` | Marital status   | At study entry: 1 = Married (n = 245), 0 = not (n = 155)
`typeca`  | Type of cancer   | 3 categories: 1 = GI/colorectal (n = 177), 2 = Lung (n = 129), 3 = GYN (n = 94). 
`stprob`  | 5-year survival  | Model probability of 5-year survival, based on type and stage of cancer. Observed range: 0.01, 0.72
`charlson` | Charlson score  | Comorbidity index at baseline: higher scores indicate greater comorbidity. Observed range: 0-7.
`ecog`    | ECOG score       | 0 = fully active, 1 = restricted regarding physically strenuous activity, 2 = ambulatory, can self-care, otherwise limited, 3 = capable of only limited self-care.
`alive`   | Mortality Status | Alive at study conclusion & 1 = alive (n = 245), 0 = dead (n = 155)
`hospice` | Hospice Status | Entered hospice before death or study end & 1 = hospice (n = 143), 0 = no (n = 257)

Note: You are welcome to treat `ecog` and `charlson` as either quantitative or categorical variables in developing your response. 

## Task 1.

Ignoring the covariate information, provide an appropriate (unadjusted) estimate (with point estimate and 95\% confidence interval) of the effect of the intervention on each of the two binary outcomes; first survival, and then hospice entry. Be sure to describe the effect in English sentences, so that both the direction and magnitude are clear, and also be sure to specify the method you used in generating your estimates. 

## Task 2. 

Next, fit a propensity score model to the data, using the eight pieces of covariate information, including age, gender, race, marital status, cancer type (which must be treated in R as a factor rather than just a continuous predictor) the model survival probability, Charlson index and ECOG. Do not include interactions between terms.

## Task 3.

Evaluate Rubin's Rule 1 and Rubin's Rule 2 for the data taken as a whole. What can you conclude about the balance across the two exposure groups prior to using the propensity score? What do these results suggest about your model in Task 1?

## Task 4.

Use direct adjustment for the (logit of) the propensity score in a logistic regression model for the `hospice` outcome to evaluate the intervention's effect on hospice entry, developing a point estimate (this should be an odds ratio) and a 95\% confidence interval. 

## Task 5.

Use subclassification by quintile of the propensity score to estimate the effect of the intervention on hospice entry. Specifically, first report an odds ratio estimate (and confidence interval) for each individual stratum, then demonstrate a pooled estimate across all five strata, being sure to indicate whether you believe pooling to be appropriate in this setting.

## Task 6. 

In our first propensity score matching attempt with the `canc3` data, we'll apply a 1:1 match without replacement. Do the matching, and then evaluate the balance associated with this approach, as follows.

### Task 6a.

Evaluate the degree of covariate imbalance before and after propensity score matching for each of the eight covariates and for the (linear *and* raw) propensity score. Do so by plotting the standardized differences. Your plot should include standardized differences that identify the three cancer types (one remaining as baseline) individually, one each for any other covariates you treat as quantitative, and an appropriate set of indicators for any others you treat as categorical, plus one for the linear propensity score, and one for the raw propensity score.

### Task 6b.

Evaluate the balance imposed by your 1:1 match via calculation of Rubin's Rule 1 and Rule 2 results, and comparing them to our results obtained prior to propensity adjustment in  Task 3.

### Task 6c.

Finally, find a point estimate (and 95\% confidence interval) for the effect of the treatment on the `hospice` outcome, based on your 1:1 match on the propensity score. Since the outcomes are binary, you should be using a conditional logistic regression to establish odds ratio estimates, while accounting for the pairs.

## Task 7.

Compare your unadjusted (Task 1), propensity score-adjusted (by regression: Task 4), propensity score subclassification (Task 5) and propensity matching (Task 6) estimates of the effect of the intervention on the `hospice` outcome in a table (or better, graph.) What can you conclude?
