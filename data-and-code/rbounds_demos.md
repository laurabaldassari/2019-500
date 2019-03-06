Using rbounds with simulated data
================
Thomas E. Love
2019-03-06

Setup
=====

``` r
knitr::opts_chunk$set(comment = NA)
```

``` r
library(Matching)
```

    Loading required package: MASS

    ## 
    ##  Matching (Version 4.9-3, Build Date: 2018-05-03)
    ##  See http://sekhon.berkeley.edu/matching for additional documentation.
    ##  Please cite software as:
    ##   Jasjeet S. Sekhon. 2011. ``Multivariate and Propensity Score Matching
    ##   Software with Automated Balance Optimization: The Matching package for R.''
    ##   Journal of Statistical Software, 42(7): 1-52. 
    ##

``` r
library(rbounds)
library(janitor)
library(tidyverse)
```

    -- Attaching packages --------------------------------------------------------------------------- tidyverse 1.2.1 --

    v ggplot2 3.1.0     v purrr   0.3.0
    v tibble  2.0.1     v dplyr   0.7.8
    v tidyr   0.8.2     v stringr 1.3.1
    v readr   1.3.1     v forcats 0.3.0

    -- Conflicts ------------------------------------------------------------------------------ tidyverse_conflicts() --
    x dplyr::filter() masks stats::filter()
    x dplyr::lag()    masks stats::lag()
    x dplyr::select() masks MASS::select()

``` r
sim_obs <- read_csv("sim_obs.csv") %>% clean_names()
```

    Parsed with column specification:
    cols(
      id = col_double(),
      treated = col_double(),
      out1 = col_double(),
      ps = col_double(),
      out2 = col_double(),
      censor = col_double(),
      out3 = col_double()
    )

``` r
sim_obs
```

    # A tibble: 500 x 7
          id treated  out1    ps  out2 censor  out3
       <dbl>   <dbl> <dbl> <dbl> <dbl>  <dbl> <dbl>
     1  1001       1     1 0.809 202.       0   897
     2  1002       1     1 0.444 120.       0   725
     3  1003       0     1 0.486 284.       0   390
     4  1004       0     0 0.306 404.       1   266
     5  1005       0     1 0.102 138.       0    57
     6  1006       0     0 0.529 231.       0   108
     7  1007       1     0 0.427 250.       1   545
     8  1008       1     1 0.337 245.       0   663
     9  1009       0     0 0.192 273.       0   316
    10  1010       1     1 0.352  85.6      0   689
    # ... with 490 more rows

Binary Outcome (1:1 Match)
==========================

``` r
m.obj <- Match(Y = sim_obs$out1, 
               Tr = as.logical(sim_obs$treated), 
               X = sim_obs$ps, 
               M = 1, replace = FALSE)

summary(m.obj)
```


    Estimate...  0.14 
    SE.........  0.042351 
    T-stat.....  3.3057 
    p.val......  0.00094735 

    Original number of observations..............  500 
    Original number of treated obs...............  250 
    Matched number of observations...............  250 
    Matched number of observations  (unweighted).  250 

Estimating *Γ* with `binarysens`
--------------------------------

``` r
binarysens(m.obj, Gamma = 3, GammaInc = 0.25)
```


     Rosenbaum Sensitivity Test 
     
    Unconfounded estimate ....  8e-04 

     Gamma Lower bound Upper bound
      1.00     0.00078     0.00078
      1.25     0.00001     0.02456
      1.50     0.00000     0.15860
      1.75     0.00000     0.42373
      2.00     0.00000     0.69087
      2.25     0.00000     0.86422
      2.50     0.00000     0.94847
      2.75     0.00000     0.98232
      3.00     0.00000     0.99432

     Note: Gamma is Odds of Differential Assignment To
     Treatment Due to Unobserved Factors 
     

The Matched Sample
------------------

``` r
matches <- factor(rep(m.obj$index.treated, 2))
sim.matchedsample1 <- cbind(matches, sim_obs[c(m.obj$index.control, m.obj$index.treated),])

head(sim.matchedsample1)
```

      matches   id treated out1    ps  out2 censor out3
    1       1 1370       0    0 0.808 341.5      1  492
    2       2 1223       0    1 0.444 284.4      0  406
    3       7 1113       0    0 0.427 446.1      0  731
    4       8 1116       0    1 0.340 369.2      0  719
    5      10 1402       0    1 0.352  74.7      1  247
    6      12 1256       0    1 0.580 128.1      0  739

``` r
tmp <- sim.matchedsample1 %>% mutate(res = 10*treated + out1) %>%
    group_by(matches) %>%
    summarize(out.tr = out1[2], out.ctrl = out1[1]) 
```

``` r
tmp %>% tabyl(out.tr, out.ctrl) %>% adorn_title()
```

            out.ctrl   
     out.tr        0  1
          0       34 41
          1       76 99

So our 2x2 table would be:

|           2x2 Table|  Treated has `out1`|  Treated no `out1`|
|-------------------:|-------------------:|------------------:|
|  Control has `out1`|                  99|                 41|
|   Control no `out1`|                  76|                 34|

Continuous Outcome (1:1 Match)
==============================

``` r
m.obj2 <- Match(Y = sim_obs$out2, 
               Tr = as.logical(sim_obs$treated), 
               X = sim_obs$ps, 
               M = 1, replace = FALSE)

summary(m.obj2)
```


    Estimate...  -72.984 
    SE.........  9.2781 
    T-stat.....  -7.8663 
    p.val......  3.5527e-15 

    Original number of observations..............  500 
    Original number of treated obs...............  250 
    Matched number of observations...............  250 
    Matched number of observations  (unweighted).  250 

``` r
psens(m.obj2, Gamma = 3, GammaInc = 0.25)
```


     Rosenbaum Sensitivity Test for Wilcoxon Signed Rank P-Value 
     
    Unconfounded estimate ....  0 

     Gamma Lower bound Upper bound
      1.00           0      0.0000
      1.25           0      0.0000
      1.50           0      0.0000
      1.75           0      0.0005
      2.00           0      0.0066
      2.25           0      0.0386
      2.50           0      0.1274
      2.75           0      0.2833
      3.00           0      0.4770

     Note: Gamma is Odds of Differential Assignment To
     Treatment Due to Unobserved Factors 
     

Rosenbaum Bounds for Hodges-Lehmann Point Estimate
--------------------------------------------------

``` r
hlsens(m.obj2, pr = 0.1, Gamma = 3, GammaInc = 0.25)
```


     Rosenbaum Sensitivity Test for Hodges-Lehmann Point Estimate 
     
    Unconfounded estimate ....  -72.6 

     Gamma Lower bound Upper bound
      1.00       -72.6   -72.60000
      1.25       -87.1   -57.50000
      1.50       -99.6   -45.50000
      1.75      -109.7   -35.00000
      2.00      -118.4   -26.20000
      2.25      -126.2   -18.80000
      2.50      -132.6   -12.20000
      2.75      -138.8    -6.20000
      3.00      -144.8    -0.70004

     Note: Gamma is Odds of Differential Assignment To
     Treatment Due to Unobserved Factors
