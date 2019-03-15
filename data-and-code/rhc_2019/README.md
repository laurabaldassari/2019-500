# Demonstrating Various Propensity Analyses using the Right Heart Catheterization data

This example uses real data from the SUPPORT study, describing analyses related to the causal effects of right heart catheterization in critically ill patients.

- The [R Markdown code](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/01_rhc_2019.Rmd)
- A [Github Markdown result](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/01_rhc_2019.md)
- The HTML version is most easily [viewed via RPubs](http://rpubs.com/TELOVE/rhc-500-2019) at http://rpubs.com/TELOVE/rhc-500-2019
- The [clean Rds data set](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/rhc.Rds), and the [original .csv data](https://github.com/THOMASELOVE/2019-500/blob/master/data-and-code/rhc_2019/rhc.csv) (and those data are [also housed at Vanderbilt](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/DataSets/rhc.csv), with [this description](http://biostat.mc.vanderbilt.edu/wiki/pub/Main/DataSets/rhc.html)).

This example will be our primary topic of conversation in Class on 2019-03-21.

To run this yourself, create a new directory for an R studio project, then place the R Markdown code in a subdirectory of that directory called R and also create an (empty) subdirectory called data. That should do it.

The example demonstrates:

1. Working with real data
2. Using various approaches to matching with the propensity score (from the Matching package)
3. Assessing covariate balance after matching
4. Working with a binary outcome, a quantitative outcome and a survival (time-to-event) outcome
5. Sensitivity analyses after matching
