# Demonstrating Various Propensity Analyses using the Right Heart Catheterization data

This example uses real data from the SUPPORT study, describing analyses related to the causal effects of right heart catheterization in critically ill patients.

- The [R Markdown code](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/01_rhc_2019.Rmd)
- A [Github Markdown result](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/01_rhc_2019.md)
- The HTML version is most easily [viewed via RPubs](http://rpubs.com/TELOVE/rhc-500-2019) at http://rpubs.com/TELOVE/rhc-500-2019
- The [clean Rds data set](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/rhc.Rds), and the [original .csv data](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/rhc.csv) (and those data are [also housed at Vanderbilt](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/DataSets/rhc.csv), with [this description](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/DataSets/rhc.html)).

This example will be our primary topic of conversation in Class on 2019-03-21.

## Post-Class Update

The latest version makes the following changes:

1. Leave outcomes out of initial runs for each match, and return them for sensitivity analyses.
2. Reduce the vertical size of the Love plots a bit.
3. Set a seed explicitly.
4. Fix errors in the sensitivity analysis presentation for binary and quantitative outcomes.
5. Fix error in specifying Match 4 so that now it is looking at "with" replacement.
6. Fix error in title of Match 5 so it now correctly specifies "without" replacement.

Still to be done:

1. Run this again, with R version 3.5.3.
2. Remove warning messages.
3. Perhaps switch Matches 4 and 5 so that the ordering makes more sense (without replacement, then with replacement)
4. More explicit description of exactly what's happening in each match.


## Running This Yourself

To run this yourself, create a new directory for an R studio project, then place the R Markdown code in a subdirectory of that directory called R and also create an (empty) subdirectory called data. That should do it.

The example demonstrates:

1. Working with real data
2. Using various approaches to matching with the propensity score (from the Matching package)
3. Assessing covariate balance after matching
4. Working with a binary outcome, a quantitative outcome and a survival (time-to-event) outcome
5. Sensitivity analyses after matching
