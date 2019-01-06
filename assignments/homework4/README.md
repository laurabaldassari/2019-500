# Homework 4 for 500 (Due 2018-03-21)

## Submission Details

Submit your work via [Canvas](https://canvas.case.edu/) before noon on 2019-03-21.

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

This assignment asks you to run propensity score weighting (with two different ATT approaches) for the `canc3` data that you studied in Assignment 3.

## Task 1. 

Execute weighting by the inverse propensity score, using the ATT approach (weight 1 for all intervention patients and weight `ps/(1-ps)` for all controls.) Plot the weights you applied within the intervention and control groups. Briefly explain what's happening.

## Task 2. 

Use the `twang` package's `dx.wts` function to start assessing balance after weighting. What is the effective sample size within the control group after weighting? Can you explain what this value means, briefly?

## Task 3.

Use the `bal.table` function to list (among other things) the standardized effect sizes for your covariate list. What can you conclude about the standardized differences (i.e. 100* the standardized effect sizes) across our covariates? Plot these standardized differences in a Love plot, along with the standardized differences prior to propensity adjustment that you developed in Assignment 3. Are you satisfied with the balance after weighting here?

## Task 4.

Evaluate Rubin's Rule 1 and Rule 2 for the post-weighting covariate distributions. Do the results seem satisfactory?

## Task 5.

Now use the `twang` package to create both the propensity scores (using generalized boosted modeling) and the ATT weights. Compare your results from Tasks 1-4 to your result here in terms of:

- a. effective sample size
- b. balance as described by the Love plot and standardized differences

## Task 6.

Select the weighting approach (of the two you have developed) that you prefer, and use it to find propensity-weighted estimates of the intervention effect on survival **and** on hospice. Your results should include a properly labeled point estimate and associated confidence interval for each outcome. 

## Task 7.

Next, run an analysis that combines weighting (either approach is OK) with regression adjustment for the linear propensity score to obtain a "doubly robust" set of estimates. Use this approach to again find estimates of the intervention effect on survival  **and** hospice.

## Task 8.

Finally, compare your results in Tasks 6 and 7 here to those obtained in Assignment 3 for the `hospice` outcome. What conclusions can you draw?

