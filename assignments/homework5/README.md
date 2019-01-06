# Homework 5 for 500 (Due 2019-04-04)

## Submission Details

Submit your work via [Canvas](https://canvas.case.edu/) before noon on 2019-04-04.

Again, I recommend a close look at [the toy example](https://github.com/THOMASELOVE/500-2018/tree/master/data-and-code/toy_example) and other examples from our [Data and Code page](https://github.com/THOMASELOVE/500-2018/tree/master/data-and-code).

## Requirements

Develop an analysis of the data in the DIG teaching data set we looked at in Homeworks 1 and 2. Choose a population (based on the available DIG data or an appropriate subset), outcome, a binary indicator of treatment/exposure group and a set of between 10 and 30 covariates, then produce a R Markdown and HTML file combination which addresses Tasks 1-5 below.

### Task 1. 

Build and display an appropriate Table 1 comparing the treatment groups on the covariates of interest.

### Task 2.

Build and describe an unadjusted analysis of the impact of the treatment on the outcome. This should yield both a point estimate and uncertainty interval.

### Task 3. 

Build a complete analysis using propensity matching, including a balance assessment pre- and post-matching, and an appropriate matched-set estimate and uncertainty interval for the causal effect of treatment on outcome, in the population you have defined, accompanied by a sensitivity analysis if the results appear significant, and a smart stability analysis if the results do not appear to be significant.

### Task 4.

Build a complete analysis using propensity weighting (and regression adjustment, if you like), including a balance assessment pre- and post-matching, and an appropriate propensity-weighted estimate and uncertainty interval for the causal effect of treatment on outcome, in the population you have defined.

### Task 5. 

Build and describe (in complete English sentences) a comparison of the results obtained from Tasks 2, 3 and 4. Describe any concerns you have about the relative merits of your various causal effect estimates.

