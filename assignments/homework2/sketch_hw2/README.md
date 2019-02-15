500 Homework 2 Answer Sketch
================
Thomas E. Love
due 2019-02-07 (version: 2019-01-25)

-   [Setup and Loading Packages](#setup-and-loading-packages)
-   [1. Create a sample of 1000 subjects](#create-a-sample-of-1000-subjects)
-   [2. Create a Table 1.](#create-a-table-1.)
    -   [Data Cleaning / Factor Labeling](#data-cleaning-factor-labeling)
    -   [Summary of the Cleaned Data](#summary-of-the-cleaned-data)
    -   [Resulting Table 1.](#resulting-table-1.)
-   [3. Build a logistic regression model.](#build-a-logistic-regression-model.)
    -   [A potentially important tangent](#a-potentially-important-tangent)
-   [4. Redefine sample and rebuild Table/Model.](#redefine-sample-and-rebuild-tablemodel.)
    -   [The New Sample](#the-new-sample)
    -   [The New Table 1](#the-new-table-1)
    -   [The New Logistic Regression Model](#the-new-logistic-regression-model)
-   [5. Add fitted probabilities, then plot against observed status.](#add-fitted-probabilities-then-plot-against-observed-status.)
    -   [Adding the Fitted Probabilities](#adding-the-fitted-probabilities)
    -   [Building a Plot](#building-a-plot)

Setup and Loading Packages
--------------------------

``` r
library(tableone); library(skimr); library(janitor)
library(tidyverse)
```

    -- Attaching packages ------------------------------------------------------------ tidyverse 1.2.1 --

    v ggplot2 3.1.0     v purrr   0.2.5
    v tibble  2.0.1     v dplyr   0.7.8
    v tidyr   0.8.2     v stringr 1.3.1
    v readr   1.3.1     v forcats 0.3.0

    -- Conflicts --------------------------------------------------------------- tidyverse_conflicts() --
    x dplyr::filter() masks stats::filter()
    x dplyr::lag()    masks stats::lag()

``` r
skim_with(numeric = list(hist = NULL))
```

1. Create a sample of 1000 subjects
===================================

Create a sample of 1000 subjects from the `dig1.csv` data describing the DIG study. Specify a random seed (via `set.seed`) to select your sample of 1000 subjects. Ensure that your sample does not include any subject who has missing information on the indicator of previous myocardial infarction, `PREVMI`. (You may want to identify such subjects in advance and filter them out of the dig1 data before you sample.)

So, we'll filter out anyone with missing `PREVMI` first.

``` r
dig1_raw <- read_csv("dig1.csv") %>%
    filter(!is.na(PREVMI))
```

    Parsed with column specification:
    cols(
      .default = col_double()
    )

    See spec(...) for full column specifications.

``` r
dig1_raw %>% skim(PREVMI)
```

    Skim summary statistics
     n obs: 6799 
     n variables: 72 

    -- Variable type:numeric ----------------------------------------------------------------------------
     variable missing complete    n mean   sd p0 p25 p50 p75 p100
       PREVMI       0     6799 6799 0.65 0.48  0   0   1   1    1

``` r
set.seed(500)

dig2 <- dig1_raw %>% 
    sample_n(size = 1000) %>%
    clean_names()

dig2
```

    # A tibble: 1,000 x 72
       subjectid trtmt   age  race   sex ejf_per ejfmeth chestx   bmi klevel
           <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>   <dbl>  <dbl> <dbl>  <dbl>
     1      5669     1    67     1     2      44       3  0.51   25.6    4.2
     2      4930     1    41     1     1      23       2  0.49   32.5    5.3
     3      6631     1    49     1     1      24       1  0.5    21.3   NA  
     4      3179     1    56     1     1      21       1  0.45   26.3    3.7
     5      5521     0    72     1     1      17       1  0.5    25.1   NA  
     6      1399     0    74     1     1      31       1  0.47   21.3   NA  
     7      3481     0    56     2     1      25       1  0.570  20.3    4.7
     8      6287     0    67     1     1      32       3  0.5    34.2    4.2
     9      5630     0    68     1     1      26       3  0.41   24.8    5.1
    10      4833     1    60     1     1      25       1  0.570  29.4    5.5
    # ... with 990 more rows, and 62 more variables: creat <dbl>,
    #   digdoser <dbl>, chfdur <dbl>, rales <dbl>, elevjvp <dbl>,
    #   pedema <dbl>, restdys <dbl>, exertdys <dbl>, actlimit <dbl>, s3 <dbl>,
    #   pulcong <dbl>, nsym <dbl>, heartrte <dbl>, diabp <dbl>, sysbp <dbl>,
    #   functcls <dbl>, chfetiol <dbl>, prevmi <dbl>, angina <dbl>,
    #   diabetes <dbl>, hyperten <dbl>, diguse <dbl>, diuretk <dbl>,
    #   diuret <dbl>, ksupp <dbl>, aceinhib <dbl>, nitrates <dbl>,
    #   hydral <dbl>, vasod <dbl>, digdose <dbl>, cvd <dbl>, cvddays <dbl>,
    #   whf <dbl>, whfdays <dbl>, dig <dbl>, digdays <dbl>, mi <dbl>,
    #   midays <dbl>, uang <dbl>, uangdays <dbl>, strk <dbl>, strkdays <dbl>,
    #   sva <dbl>, svadays <dbl>, vena <dbl>, venadays <dbl>, crev <dbl>,
    #   crevdays <dbl>, ocvd <dbl>, ocvddays <dbl>, rinf <dbl>,
    #   rinfdays <dbl>, oth <dbl>, othdays <dbl>, hosp <dbl>, hospdays <dbl>,
    #   nhosp <dbl>, death <dbl>, deathday <dbl>, reason <dbl>, dwhf <dbl>,
    #   dwhfdays <dbl>

2. Create a Table 1.
====================

The Table 1 should describe the data according to whether or not the subject had a previous myocardial infarction (`prevmi`) across each of these 12 variables.

|    Variable| Description                                                    |
|-----------:|----------------------------------------------------------------|
|     `trtmt`| Treatment group (1 = DIG, 0 = Placebo)                         |
|       `age`| Age in years                                                   |
|      `race`| White (1) or Non-White (2)                                     |
|       `sex`| Male (1) or Female (2)                                         |
|   `ejf_per`| Ejection Fraction (percent)                                    |
|    `chestx`| Chest X-ray (CT ratio)                                         |
|       `bmi`| Body-Mass Index                                                |
|    `klevel`| Serum Potassium level (mEq/l)                                  |
|     `creat`| Serum Creatinine level (mg/dl)                                 |
|    `chfdur`| Approximate Duration of CHF (mos.)                             |
|  `exertdys`| Dyspnea on exertion (see note)                                 |
|  `functcls`| Current NYHA Functional Class (1 = I, 2 = II, 3 = III, 4 = IV) |

Note that the `dyspnea` categories are: 0 = None or Unknown, 1 = Present, 2 = Past, 3 = Present and Past

Data Cleaning / Factor Labeling
-------------------------------

Be sure to correctly represent each of the categorical variables as factors, rather than in the numerical form they start in. Label your factors to ease the work for the viewer, and reduce or eliminate the need to look at a codebook. Also, be sure to accurately report whether any missing values are observed in this sample.

*Note*: You're going to have to do this again with a revised sample in step 4, so it's worth it to code this in a reproducible way.

``` r
dig2a <- dig2 %>%
    mutate(prevmi_f = fct_recode(factor(prevmi), 
                                 Yes = "1",
                                 No = "0"),
           prevmi_f = fct_relevel(prevmi_f, "Yes"),
           treat_f = fct_recode(factor(trtmt), 
                                DIG = "1",
                                Placebo = "0"),
           race_f = fct_recode(factor(race), 
                               White = "1", 
                               "Non-white" = "2"),
           race_f = fct_relevel(race_f, "Non-white"),
           sex_f = fct_recode(factor(sex),
                              F = "1",
                              M = "2"),
           sex_f = fct_relevel(sex_f, "M"),
           dyspnea_f = fct_recode(factor(exertdys),
                                  None_or_Unknown = "0",
                                  Present = "1",
                                  Past = "2",
                                  Present_and_Past = "3"),
           dyspnea_f = fct_relevel(dyspnea_f,
                                   "None_or_Unknown", 
                                   "Past", "Present"),
           nyha_f = fct_recode(factor(functcls), 
                                I = "1",
                                II = "2",
                                III = "3",
                                IV = "4")) %>%
    
    select(subjectid, prevmi, prevmi_f, treat_f, age, 
           race_f, sex_f, ejf_per, chestx, bmi, klevel, 
           creat, chfdur, dyspnea_f, nyha_f)
```

Summary of the Cleaned Data
---------------------------

``` r
summary(dig2a)
```

       subjectid        prevmi      prevmi_f     treat_f         age       
     Min.   :  12   Min.   :0.000   Yes:647   Placebo:533   Min.   :24.00  
     1st Qu.:1679   1st Qu.:0.000   No :353   DIG    :467   1st Qu.:57.00  
     Median :3459   Median :1.000                           Median :64.00  
     Mean   :3429   Mean   :0.647                           Mean   :62.99  
     3rd Qu.:5158   3rd Qu.:1.000                           3rd Qu.:70.00  
     Max.   :6797   Max.   :1.000                           Max.   :94.00  
                                                                           
           race_f    sex_f      ejf_per          chestx            bmi       
     Non-white:142   M:202   Min.   : 3.00   Min.   :0.1500   Min.   :14.92  
     White    :858   F:798   1st Qu.:21.00   1st Qu.:0.4900   1st Qu.:23.44  
                             Median :29.00   Median :0.5300   Median :26.52  
                             Mean   :28.49   Mean   :0.5341   Mean   :27.07  
                             3rd Qu.:35.00   3rd Qu.:0.5800   3rd Qu.:29.70  
                             Max.   :45.00   Max.   :0.8200   Max.   :49.26  
                                                                             
         klevel          creat           chfdur                  dyspnea_f  
     Min.   :0.000   Min.   :0.600   Min.   :  0.00   None_or_Unknown : 40  
     1st Qu.:4.050   1st Qu.:1.023   1st Qu.:  5.00   Past            :208  
     Median :4.300   Median :1.200   Median : 16.00   Present         :168  
     Mean   :4.333   Mean   :1.282   Mean   : 29.06   Present_and_Past:582  
     3rd Qu.:4.600   3rd Qu.:1.443   3rd Qu.: 38.00   NA's            :  2  
     Max.   :5.800   Max.   :3.000   Max.   :360.00                         
     NA's   :125                     NA's   :1                              
     nyha_f   
     I  :121  
     II :571  
     III:283  
     IV : 25  
              
              
              

And we can summarize the missingness in our sample of 1,000 people as:

-   125 missing `klevel` values,
-   1 missing `chfdur` value, and
-   2 missing `dyspnea_f` status

Resulting Table 1.
------------------

``` r
q2_t1 <- CreateTableOne(data = dig2a, 
                    vars = c("treat_f", "age", "race_f", 
                             "sex_f", "ejf_per", "chestx", 
                             "bmi", "klevel", "creat", 
                             "chfdur", "dyspnea_f", "nyha_f"),
                    strata = c("prevmi_f"))
q2_t1
```

                         Stratified by prevmi_f
                          Yes           No            p      test
      n                     647           353                    
      treat_f = DIG (%)     311 (48.1)    156 (44.2)   0.268     
      age (mean (sd))     63.21 (11.04) 62.60 (10.64)  0.404     
      race_f = White (%)    555 (85.8)    303 (85.8)   1.000     
      sex_f = F (%)         522 (80.7)    276 (78.2)   0.392     
      ejf_per (mean (sd)) 28.45 (8.91)  28.56 (9.10)   0.852     
      chestx (mean (sd))   0.54 (0.07)   0.53 (0.07)   0.141     
      bmi (mean (sd))     27.20 (4.97)  26.82 (4.92)   0.244     
      klevel (mean (sd))   4.31 (0.53)   4.38 (0.44)   0.064     
      creat (mean (sd))    1.29 (0.36)   1.27 (0.36)   0.632     
      chfdur (mean (sd))  29.22 (35.52) 28.76 (36.48)  0.845     
      dyspnea_f (%)                                    0.482     
         None_or_Unknown     27 ( 4.2)     13 ( 3.7)             
         Past               136 (21.1)     72 (20.5)             
         Present            100 (15.5)     68 (19.3)             
         Present_and_Past   383 (59.3)    199 (56.5)             
      nyha_f (%)                                       0.505     
         I                   81 (12.5)     40 (11.3)             
         II                 361 (55.8)    210 (59.5)             
         III                186 (28.7)     97 (27.5)             
         IV                  19 ( 2.9)      6 ( 1.7)             

There are lots of other things we could do here, including:

-   making decisions about Normality for each quantitative variable, which might then lead us to summarize some quantitative variables with medians and quartiles, rather than means and standard deviations, and using Wilcoxon rank sum rather than t tests for p values,
    -   an interesting idea is using the `skim` function's histograms after grouping the data by `prevmi_f` to scan and make these decisions,
    -   or we could use summary applied to the tableone object and compare the p values we would obtain in either case (if the p values are similar, then the choice must not make much of a difference)
    -   or we could work our way through a series of more serious Normality checks, with histograms, boxplots, Normal Q-Q plots, etc.
-   assessing whether an exact or approximate test might be a better choice for each categorical variable, but that's a small issue.
-   another approach would have been to leave the factor variables as they were originally and simply specify some as factors in the call to CreateTableOne. That would have left us with some tougher-to-interpret level names and orders, though.

For now, I'll just leave it as it is.

3. Build a logistic regression model.
=====================================

Build a logistic regression model for previous MI using the main effects of the 12 variables above. I'd call the model `m1` that predicts the log odds of previous myocardial infarction (`prevmi`) on the basis of the main effects of each of the twelve variables in your table above, for your sample of 1000 subjects. How many observations does your model actually fit results for? (This is asking for the number of subjects without any missingness, across all variables in your model.)

``` r
m1 <- glm(prevmi ~ treat_f + age + race_f + sex_f +
              ejf_per + chestx + bmi + klevel +
              creat + chfdur + dyspnea_f + nyha_f,
          data = dig2a, family = binomial(link = logit))

summary(m1)
```


    Call:
    glm(formula = prevmi ~ treat_f + age + race_f + sex_f + ejf_per + 
        chestx + bmi + klevel + creat + chfdur + dyspnea_f + nyha_f, 
        family = binomial(link = logit), data = dig2a)

    Deviance Residuals: 
        Min       1Q   Median       3Q      Max  
    -1.8589  -1.3446   0.8289   0.9516   1.3221  

    Coefficients:
                                Estimate Std. Error z value Pr(>|z|)  
    (Intercept)                0.0089975  1.3196111   0.007   0.9946  
    treat_fDIG                 0.2989715  0.1456329   2.053   0.0401 *
    age                        0.0021372  0.0066163   0.323   0.7467  
    race_fWhite               -0.0465217  0.2256648  -0.206   0.8367  
    sex_fF                     0.2423509  0.1852287   1.308   0.1907  
    ejf_per                   -0.0021148  0.0084681  -0.250   0.8028  
    chestx                     1.6182985  1.0971730   1.475   0.1402  
    bmi                        0.0198079  0.0148391   1.335   0.1819  
    klevel                    -0.2667290  0.1551576  -1.719   0.0856 .
    creat                      0.1205537  0.2043800   0.590   0.5553  
    chfdur                     0.0007344  0.0020288   0.362   0.7174  
    dyspnea_fPast             -0.1892549  0.4068272  -0.465   0.6418  
    dyspnea_fPresent          -0.5244456  0.4078396  -1.286   0.1985  
    dyspnea_fPresent_and_Past -0.1389377  0.3844295  -0.361   0.7178  
    nyha_fII                  -0.0135288  0.2298261  -0.059   0.9531  
    nyha_fIII                  0.1320892  0.2531865   0.522   0.6019  
    nyha_fIV                   0.5799252  0.5654448   1.026   0.3051  
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    (Dispersion parameter for binomial family taken to be 1)

        Null deviance: 1130.1  on 871  degrees of freedom
    Residual deviance: 1109.7  on 855  degrees of freedom
      (128 observations deleted due to missingness)
    AIC: 1143.7

    Number of Fisher Scoring iterations: 4

The sample size used by this model is 872 subjects. We know this because the output tells us that 128 of our original 1000 observations were deleted due to missingness, or because the null deviance is associated with 871 degrees of freedom, and the null deviance will always be associated with n - 1 degrees of freedom, where n is the number of observations actually used to fit the model.

-   Another way of determining the number of observations with complete data across all variables in the `dig2a` data is to use `count` and `complete.cases` like this:

``` r
dig2a %>% count(complete.cases(.))
```

    # A tibble: 2 x 2
      `complete.cases(.)`     n
      <lgl>               <int>
    1 FALSE                 128
    2 TRUE                  872

A potentially important tangent
-------------------------------

When fitting a logistic regression model in R, how do you know which level of your binary response (1 or 0, Yes or No, etc.) is being predicted by the `glm`?

Let's show a simple case.

``` r
toy1 <- dig2a %>% select(prevmi, prevmi_f, treat_f, bmi)

toy_modelA <- glm(prevmi ~ treat_f + bmi, 
                  data = toy1, 
                  family = binomial(link = logit))

toy_modelB <- glm(prevmi_f ~ treat_f + bmi, 
                  data = toy1, 
                  family = binomial(link = logit))

toy_modelA
```


    Call:  glm(formula = prevmi ~ treat_f + bmi, family = binomial(link = logit), 
        data = toy1)

    Coefficients:
    (Intercept)   treat_fDIG          bmi  
        0.08344      0.16351      0.01655  

    Degrees of Freedom: 999 Total (i.e. Null);  997 Residual
    Null Deviance:      1299 
    Residual Deviance: 1296     AIC: 1302

``` r
toy_modelB
```


    Call:  glm(formula = prevmi_f ~ treat_f + bmi, family = binomial(link = logit), 
        data = toy1)

    Coefficients:
    (Intercept)   treat_fDIG          bmi  
       -0.08344     -0.16351     -0.01655  

    Degrees of Freedom: 999 Total (i.e. Null);  997 Residual
    Null Deviance:      1299 
    Residual Deviance: 1296     AIC: 1302

As you can see, the coefficients in `toy_modelA` are the negative of the coefficients in `toy_modelB`. This is because one of the models (model A, as it turns out) is estimating Pr(Previous MI) and one (model B, as it turns out) is estimating Pr(No previous MI). How do we know for sure which is which?

-   R, by default for a logistic regression using `glm`, wants a numeric response with 1 for "success" and 0 for "failure" and it will fit a model to predict the probability of "success".
-   For logistic regression models, `glm` will also accept a factor response, where the first level denotes "failure" and all other levels denote "success".

In general...

-   if we use a 1/0 numeric outcome like `PREVMI`, we will get Pr(PREVMI = 1) from our model.
-   if we use a factor outcome like `prevmi_f`, we should look at the order of the levels - whatever is first will be treated as "failure" and the rest as "success", and we will get Pr("success") from our model.

To check the levels of a factor, we can use `levels` or `table`, for example.

``` r
levels(toy1$prevmi_f)
```

    [1] "Yes" "No" 

``` r
table(toy1$prevmi_f)
```


    Yes  No 
    647 353 

Here, in either case, we see the problem, which is that we've specified "Yes" as the first level and "No" as the second level. So our model fits the probability of "No". We could change this order back using `fct_relevel` if we like. Note that the order we wanted in Table 1 is the opposite of what we want for modeling.

Sometimes, people try using a logical response, like this, to deal with a factor variable.

``` r
toy_modelC <- glm((prevmi_f == "Yes") ~ treat_f + bmi, 
                  data = toy1, 
                  family = binomial(link = logit))

toy_modelC
```


    Call:  glm(formula = (prevmi_f == "Yes") ~ treat_f + bmi, family = binomial(link = logit), 
        data = toy1)

    Coefficients:
    (Intercept)   treat_fDIG          bmi  
        0.08344      0.16351      0.01655  

    Degrees of Freedom: 999 Total (i.e. Null);  997 Residual
    Null Deviance:      1299 
    Residual Deviance: 1296     AIC: 1302

As you can see this works, because the logical variable `(prevmi_f == "Yes")` places FALSE before TRUE, and so R's `glm` function models the probability that the statement `(prevmi_f == "Yes")` is TRUE.

``` r
table(toy1$prevmi_f == "Yes")
```


    FALSE  TRUE 
      353   647 

4. Redefine sample and rebuild Table/Model.
===========================================

Assuming you have at least one missing value in a predictor in your model for question 3, re-define your sample to include only the observations which are "complete cases" with no missingness on any of the key variables we're looking at. Specify the number of subjects (&lt; 1000) that remain in your new sample.

Now, **redo both Tasks 2 and 3** to describe this new sample and use it to fit a model. Call the new model `m2`. Verify that no missingness plagues this new model.

The New Sample
--------------

We'll build a new `dig2b` that limits us to the 872 cases with complete data.

``` r
dig2b <- dig2a %>% drop_na

nrow(dig2b)
```

    [1] 872

The New Table 1
---------------

Here's the new Table 1, restricted to these 872 people.

``` r
q4_t1 <- CreateTableOne(data = dig2b, 
                    vars = c("treat_f", "age", "race_f", 
                             "sex_f", "ejf_per", "chestx", 
                             "bmi", "klevel", "creat", 
                             "chfdur", "dyspnea_f", 
                             "nyha_f"),
                    strata = c("prevmi_f"))
q4_t1
```

                         Stratified by prevmi_f
                          Yes           No            p      test
      n                     566           306                    
      treat_f = DIG (%)     281 (49.6)    132 (43.1)   0.077     
      age (mean (sd))     62.90 (11.20) 62.61 (10.54)  0.710     
      race_f = White (%)    492 (86.9)    270 (88.2)   0.653     
      sex_f = F (%)         455 (80.4)    238 (77.8)   0.410     
      ejf_per (mean (sd)) 28.13 (8.81)  28.70 (9.12)   0.372     
      chestx (mean (sd))   0.54 (0.07)   0.53 (0.07)   0.090     
      bmi (mean (sd))     27.18 (4.94)  26.72 (4.93)   0.191     
      klevel (mean (sd))   4.32 (0.51)   4.38 (0.44)   0.083     
      creat (mean (sd))    1.28 (0.36)   1.27 (0.36)   0.624     
      chfdur (mean (sd))  29.44 (35.98) 28.50 (36.49)  0.714     
      dyspnea_f (%)                                    0.242     
         None_or_Unknown     23 ( 4.1)     11 ( 3.6)             
         Past               119 (21.0)     61 (19.9)             
         Present             89 (15.7)     65 (21.2)             
         Present_and_Past   335 (59.2)    169 (55.2)             
      nyha_f (%)                                       0.380     
         I                   66 (11.7)     37 (12.1)             
         II                 315 (55.7)    183 (59.8)             
         III                167 (29.5)     81 (26.5)             
         IV                  18 ( 3.2)      5 ( 1.6)             

The New Logistic Regression Model
---------------------------------

And here's the new model:

``` r
m2 <- glm(prevmi ~ treat_f + age + race_f + sex_f +
              ejf_per + chestx + bmi + klevel +
              creat + chfdur + dyspnea_f + nyha_f,
          data = dig2b, family = binomial(link = logit))

summary(m2)
```


    Call:
    glm(formula = prevmi ~ treat_f + age + race_f + sex_f + ejf_per + 
        chestx + bmi + klevel + creat + chfdur + dyspnea_f + nyha_f, 
        family = binomial(link = logit), data = dig2b)

    Deviance Residuals: 
        Min       1Q   Median       3Q      Max  
    -1.8589  -1.3446   0.8289   0.9516   1.3221  

    Coefficients:
                                Estimate Std. Error z value Pr(>|z|)  
    (Intercept)                0.0089975  1.3196111   0.007   0.9946  
    treat_fDIG                 0.2989715  0.1456329   2.053   0.0401 *
    age                        0.0021372  0.0066163   0.323   0.7467  
    race_fWhite               -0.0465217  0.2256648  -0.206   0.8367  
    sex_fF                     0.2423509  0.1852287   1.308   0.1907  
    ejf_per                   -0.0021148  0.0084681  -0.250   0.8028  
    chestx                     1.6182985  1.0971730   1.475   0.1402  
    bmi                        0.0198079  0.0148391   1.335   0.1819  
    klevel                    -0.2667290  0.1551576  -1.719   0.0856 .
    creat                      0.1205537  0.2043800   0.590   0.5553  
    chfdur                     0.0007344  0.0020288   0.362   0.7174  
    dyspnea_fPast             -0.1892549  0.4068272  -0.465   0.6418  
    dyspnea_fPresent          -0.5244456  0.4078396  -1.286   0.1985  
    dyspnea_fPresent_and_Past -0.1389377  0.3844295  -0.361   0.7178  
    nyha_fII                  -0.0135288  0.2298261  -0.059   0.9531  
    nyha_fIII                  0.1320892  0.2531865   0.522   0.6019  
    nyha_fIV                   0.5799252  0.5654448   1.026   0.3051  
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    (Dispersion parameter for binomial family taken to be 1)

        Null deviance: 1130.1  on 871  degrees of freedom
    Residual deviance: 1109.7  on 855  degrees of freedom
    AIC: 1143.7

    Number of Fisher Scoring iterations: 4

There's no missingness here, and our model uses all 872 complete observations, as we can see from the null deviance DF (which is n - 1).

5. Add fitted probabilities, then plot against observed status.
===============================================================

Use the model (`m2`) you built in Task 4 to add the fitted probability of previous myocardial infarction to your sample used to create `m2`. Produce an attractive and useful graphical summary of the distribution of fitted probabilities of previous myocardial infarction broken down into two categories by the patient's actual `prevmi` status in this sample. I suggest rounding the probabilities to two decimal places before graphing.

Adding the Fitted Probabilities
-------------------------------

There are several ways to add the fitted probabilities back to the data. You might use:

``` r
dig2b$m2fits <- predict(m2, type = "response")

dig2b %>% skim(m2fits)
```

    Skim summary statistics
     n obs: 872 
     n variables: 16 

    -- Variable type:numeric ----------------------------------------------------------------------------
     variable missing complete   n mean    sd   p0 p25  p50 p75 p100
       m2fits       0      872 872 0.65 0.073 0.42 0.6 0.65 0.7 0.88

Or you might use the `augment` tool from the `broom` package:

``` r
dig3 <- broom::augment(m2, type.predict = "response")

dig3 %>% skim(.fitted)
```

    Skim summary statistics
     n obs: 872 
     n variables: 20 

    -- Variable type:numeric ----------------------------------------------------------------------------
     variable missing complete   n mean    sd   p0 p25  p50 p75 p100
      .fitted       0      872 872 0.65 0.073 0.42 0.6 0.65 0.7 0.88

In either case, you need to specify "response" as the type of prediction you want in order to get fitted probabilities of previous MI, rather than the logit of those probabilities.

Building a Plot
---------------

As for a graphical summary - I'd be happy with anything that permitted easy comparison of the two density estimates. Options shown below include a comparison boxplot, facetted histograms, frequency polygons, and a violin plot.

``` r
ggplot(dig2b, aes(x = prevmi_f, y = m2fits, fill = prevmi_f)) +
    geom_boxplot() +
    guides(fill = FALSE) +
    labs(x = "Previous Myocardial Infarction?",
         y = "Model-estimated Probability of Previous MI")
```

![](README_files/figure-markdown_github/unnamed-chunk-18-1.png)

``` r
ggplot(dig2b, aes(x = m2fits, fill = prevmi_f)) +
    geom_histogram(bins = 20, col = "white") +
    guides(fill = FALSE) +
    labs(x = "Model-estimated Probability of Previous MI") +
    facet_wrap(~ prevmi_f, labeller = label_both)
```

![](README_files/figure-markdown_github/unnamed-chunk-19-1.png)

``` r
ggplot(dig2b, aes(x = m2fits, col = prevmi_f)) +
    geom_freqpoly(bins = 20, size = 1.5) +
    scale_color_discrete(name = "Previous MI?") +
    labs(x = "Model-estimated Probability of Previous MI") 
```

![](README_files/figure-markdown_github/unnamed-chunk-20-1.png)

``` r
ggplot(dig2b, aes(x = prevmi_f, y = m2fits, col = prevmi_f)) +
    geom_violin() +
    geom_boxplot(width = .2) +
    guides(col = FALSE) +
    labs(x = "Previous MI?",
         y = "Model-estimated Probability of Previous MI") 
```

![](README_files/figure-markdown_github/unnamed-chunk-21-1.png)
