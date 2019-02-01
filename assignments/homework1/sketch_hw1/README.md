500 Homework 1 Answer Sketch
================
Thomas E. Love
due 2019-01-31 (version: 2019-01-24)

-   [Task 1](#task-1)
-   [Task 2](#task-2)
-   [Task 3](#task-3)
    -   [The Problem](#the-problem)
    -   [Setup, Packages, Data Ingest](#setup-packages-data-ingest)
    -   [Preparing the Sample for Modeling](#preparing-the-sample-for-modeling)
    -   [Initial Data Summaries](#initial-data-summaries)
    -   [A "Complete Cases" Analysis and Training/Test Partition](#a-complete-cases-analysis-and-trainingtest-partition)
        -   [Fitting a Logistic Regression Model to the training sample](#fitting-a-logistic-regression-model-to-the-training-sample)
        -   [Applying the model to a test sample, and producing a graph](#applying-the-model-to-a-test-sample-and-producing-a-graph)
    -   [What if we instead dealt with missingness via simple imputation?](#what-if-we-instead-dealt-with-missingness-via-simple-imputation)
        -   [Fitting a Logistic Regression Model to the training sample](#fitting-a-logistic-regression-model-to-the-training-sample-1)
        -   [Applying the model to a test sample, and producing a graph](#applying-the-model-to-a-test-sample-and-producing-a-graph-1)

Task 1
======

Task 1 requires you to request the DIG data.

Task 2
======

In task 2 you were asked to build a mock proposal for a DIG observational study. We'll discuss those in class, and so I have no real sketch here. I expect that some of Rosenbaum's writing will be of help. The questions you needed to answer were:

1.  What comparison do you want to make? (Select a comparison different than the one made in the original DIG paper)
    -   Did patients receiving "EXPOSURE A" have lower rates of "BAD OUTCOME" than those who received "EXPOSURE B"?
2.  Why is this of interest?
    -   "OUTCOME" is important because ...
    -   "EXPOSURE" (A or B) is important because ...
    -   (*Be sure to clearly indicate what you hypothesize the effect of EXPOSURE on OUTCOME to be.*)
3.  What are the key measures - specifically, the exposure/treatment, the primary outcome, and important covariates that are available in the data to help address your question of interest?
    -   Exposure/Treatment = A or B, and be sure to specify the way in which you will know which exposure someone receives, and whether the exposure / treatment is applied using a randomized approach, or not.
    -   Outcome = ..., and be sure to specify the variables you will use to determine the outcome, as well as the *type* of outcome, be it continuous, categorical (and if categorical, binary or multi-categorical) or survival (and if survival, is censoring involved?)
    -   Covariates of interest: We'd be interested in anything related to treatment choice or to outcome. You should provide a list of such variables of interest. Remember to include **ONLY** things which are measured prior to the exposure/treatment of interest, or which are not possibly changed by it.

Task 3
======

The Problem
-----------

Here, you were to build and evaluate a logistic regression model using the DIG data.

Your model should be fitted to a random training sample of 5,000 subjects (be sure to specify the seed you used to select that sample) and then tested on the remaining 1,800 subjects, but you'll probably want to check for and deal with missingness in the entire sample before splitting into training and test groups. Your model will predict the probability that a subject in the study will die, based on:

-   the subject's assigned treatment (digoxin or placebo),
-   the subject's age at randomization,
-   race,
-   sex,
-   ejection fraction (percent),
-   calculated body mass index,
-   NYHA functional class, and
-   whether or not the subject currently has angina.

The relevant variables in the `dig1.csv` data set are therefore: `subjectid`, `DEATH`, `TRTMT`, `AGE`, `RACE`, `SEX`, `EJF_PER`, `BMI`, `FUNCTCLS`, and `ANGINA`.

Be sure to treat the categorical variables (including NYHA class, angina status, race and sex) appropriately as factors (ideally with meaningful names), and account for missingness deliberately in an appropriate way.

Your final results should include:

1.  a R Markdown file containing all of your code
2.  an HTML file with the results from your Markdown, which describes:
    1.  your sample preparation work including dealing with missingness and partitioning the data into training and test samples
    2.  your fitted logistic regression model (to your training sample)
    3.  the results of your application of your model to your test sample, which is best accomplished as a graph which shows the distribution of your model probability estimates in the "actually died" and "actually survived" groups within your test sample.

Setup, Packages, Data Ingest
----------------------------

``` r
library(skimr); library(broom); library(simputation)
library(janitor); library(tidyverse)
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
dig1 <- read_csv("dig1.csv") %>% clean_names()
```

    Parsed with column specification:
    cols(
      .default = col_double()
    )

    See spec(...) for full column specifications.

``` r
dig1
```

    # A tibble: 6,800 x 72
       subjectid trtmt   age  race   sex ejf_per ejfmeth chestx   bmi klevel
           <dbl> <dbl> <dbl> <dbl> <dbl>   <dbl>   <dbl>  <dbl> <dbl>  <dbl>
     1         1     0    66     1     1      40       2   0.5   20.1   NA  
     2         2     0    77     1     1      12       1   0.56  20.7    3.1
     3         3     0    72     1     2      36       1   0.68  25.5    5.1
     4         4     1    57     1     1      31       1   0.48  25.8   NA  
     5         5     0    74     1     1      15       1   0.53  25.7    4  
     6         6     0    69     2     2      45       1   0.7   27.8    4.3
     7         7     1    64     1     2      30       1   0.52  31.7    4.3
     8         8     1    60     2     1      39       1   0.4   25.1    5.1
     9         9     0    74     2     1      33       3   0.49  23.7    4.7
    10        10     1    64     1     2      24       1   0.52  28.7    4  
    # ... with 6,790 more rows, and 62 more variables: creat <dbl>,
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

Preparing the Sample for Modeling
---------------------------------

``` r
dig_hw1 <- dig1 %>%
    mutate(nyha = factor(functcls),
           female = sex - 1,
           race_f = fct_recode(factor(race), 
                               "White" = "1",
                               "Non-White" = "2"),
           tx_f = fct_recode(factor(trtmt), 
                                    "Placebo" = "0",
                                    "Treatment" = "1"),
           death_f = fct_recode(factor(death),
                                "Died" = "1",
                                "Survived" = "0")) %>%
    select(subjectid, death_f, tx_f, age, race_f, female,
           ejf_per, bmi, nyha, angina)
```

Initial Data Summaries
----------------------

OK. What do we have now?

``` r
skim_with(numeric = list(hist = NULL))

skim(dig_hw1 %>% select(-subjectid))
```

    Skim summary statistics
     n obs: 6800 
     n variables: 9 

    -- Variable type:factor -----------------------------------------------------------------------------
     variable missing complete    n n_unique                       top_counts
      death_f       0     6800 6800        2      Sur: 4425, Die: 2375, NA: 0
         nyha       6     6794 6800        4 2: 3664, 3: 2081, 1: 907, 4: 142
       race_f       0     6800 6800        2       Whi: 5809, Non: 991, NA: 0
         tx_f       0     6800 6800        2      Pla: 3403, Tre: 3397, NA: 0
     ordered
       FALSE
       FALSE
       FALSE
       FALSE

    -- Variable type:numeric ----------------------------------------------------------------------------
     variable missing complete    n  mean    sd    p0   p25  p50  p75  p100
          age       0     6800 6800 63.48 10.92 21    57    65   71   94   
       angina       2     6798 6800  0.27  0.44  0     0     0    1    1   
          bmi       1     6799 6800 27.11  5.19 14.45 23.68 26.5 29.8 62.66
      ejf_per       0     6800 6800 28.54  8.85  3    22    29   35   45   
       female       0     6800 6800  0.22  0.42  0     0     0    0    1   

Or, another way to see the counts of missing data:

``` r
dig_hw1 %>% map_dbl(~ sum(is.na(.)))
```

    subjectid   death_f      tx_f       age    race_f    female   ejf_per 
            0         0         0         0         0         0         0 
          bmi      nyha    angina 
            1         6         2 

Which observations are affected?

``` r
dig_hw1 %>% filter(!complete.cases(.)) %>%
    select(subjectid, bmi, nyha, angina)
```

    # A tibble: 9 x 4
      subjectid   bmi nyha  angina
          <dbl> <dbl> <fct>  <dbl>
    1       288  20.1 <NA>       0
    2       576  22.1 2         NA
    3      1172  22.2 2         NA
    4      2432  25.6 <NA>       0
    5      4941  NA   1          0
    6      5315  28.7 <NA>       0
    7      5549  28.7 <NA>       0
    8      6360  29.1 <NA>       0
    9      6417  47.0 <NA>       0

A "Complete Cases" Analysis and Training/Test Partition
-------------------------------------------------------

With so few missing values, a completely reasonable strategy would be to simply omit the missing data before splitting into training and test samples.

``` r
dig_hw1_noNA <- dig_hw1 %>% drop_na()

set.seed(20190131)
dig_hw1_train <- sample_n(dig_hw1_noNA, size = 5000)
dig_hw1_test <- anti_join(dig_hw1_noNA, dig_hw1_train)
```

    Joining, by = c("subjectid", "death_f", "tx_f", "age", "race_f", "female", "ejf_per", "bmi", "nyha", "angina")

Any missingness left that we missed?

``` r
colSums(is.na(dig_hw1_train))
```

    subjectid   death_f      tx_f       age    race_f    female   ejf_per 
            0         0         0         0         0         0         0 
          bmi      nyha    angina 
            0         0         0 

``` r
colSums(is.na(dig_hw1_test))
```

    subjectid   death_f      tx_f       age    race_f    female   ejf_per 
            0         0         0         0         0         0         0 
          bmi      nyha    angina 
            0         0         0 

### Fitting a Logistic Regression Model to the training sample

``` r
model1 <- glm(death_f ~ tx_f + age + race_f + female + 
                  ejf_per + bmi + nyha + angina, 
              family = binomial(link = "logit"),
              data = dig_hw1_train)

summary(model1)
```


    Call:
    glm(formula = death_f ~ tx_f + age + race_f + female + ejf_per + 
        bmi + nyha + angina, family = binomial(link = "logit"), data = dig_hw1_train)

    Deviance Residuals: 
        Min       1Q   Median       3Q      Max  
    -1.6623  -0.9305  -0.7524   1.2671   2.0309  

    Coefficients:
                      Estimate Std. Error z value Pr(>|z|)    
    (Intercept)      9.622e-02  2.826e-01   0.340 0.733493    
    tx_fTreatment    3.868e-02  6.091e-02   0.635 0.525458    
    age              1.827e-06  2.789e-03   0.001 0.999477    
    race_fNon-White -4.437e-02  8.768e-02  -0.506 0.612798    
    female          -2.461e-01  7.511e-02  -3.276 0.001053 ** 
    ejf_per         -3.710e-02  3.584e-03 -10.350  < 2e-16 ***
    bmi             -3.039e-03  5.911e-03  -0.514 0.607108    
    nyha2            3.342e-01  1.012e-01   3.303 0.000957 ***
    nyha3            8.378e-01  1.070e-01   7.833 4.75e-15 ***
    nyha4            1.362e+00  2.212e-01   6.155 7.50e-10 ***
    angina          -3.980e-02  6.869e-02  -0.579 0.562337    
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    (Dispersion parameter for binomial family taken to be 1)

        Null deviance: 6497.7  on 4999  degrees of freedom
    Residual deviance: 6219.1  on 4989  degrees of freedom
    AIC: 6241.1

    Number of Fisher Scoring iterations: 4

``` r
glance(model1)
```

    # A tibble: 1 x 7
      null.deviance df.null logLik   AIC   BIC deviance df.residual
              <dbl>   <int>  <dbl> <dbl> <dbl>    <dbl>       <int>
    1         6498.    4999 -3110. 6241. 6313.    6219.        4989

### Applying the model to a test sample, and producing a graph

``` r
dig_hw1_test$.fit <- predict(model1, newdata = dig_hw1_test, type = "response")

ggplot(dig_hw1_test, aes(x = death_f, y = .fit, fill = death_f)) +
  geom_boxplot() + 
  guides(fill = FALSE) +
  labs(y = "Estimated `model1` Probability of Death", 
       x = "Observed Vital Status",
       title = "Boxplot of `model1` predictions for DIG",
      subtitle = "NAs removed")
```

![](homework1_sketch_files/figure-markdown_github/unnamed-chunk-10-1.png)

What if we instead dealt with missingness via simple imputation?
----------------------------------------------------------------

As an alternative, a simple imputation might work well, too. I'll show you a simple imputation approach, making use of the `simputation` [package](https://github.com/markvanderloo/simputation), which is a good tool for simple imputation, and has [a nice vignette here](https://cran.r-project.org/web/packages/simputation/vignettes/intro.html).

``` r
str(dig_hw1)
```

    Classes 'tbl_df', 'tbl' and 'data.frame':   6800 obs. of  10 variables:
     $ subjectid: num  1 2 3 4 5 6 7 8 9 10 ...
     $ death_f  : Factor w/ 2 levels "Survived","Died": 1 2 1 1 1 1 2 1 1 1 ...
     $ tx_f     : Factor w/ 2 levels "Placebo","Treatment": 1 1 1 2 1 1 2 2 1 2 ...
     $ age      : num  66 77 72 57 74 69 64 60 74 64 ...
     $ race_f   : Factor w/ 2 levels "White","Non-White": 1 1 1 1 1 2 1 2 2 1 ...
     $ female   : num  0 0 1 0 0 1 1 0 0 1 ...
     $ ejf_per  : num  40 12 36 31 15 45 30 39 33 24 ...
     $ bmi      : num  20.1 20.7 25.5 25.8 25.7 ...
     $ nyha     : Factor w/ 4 levels "1","2","3","4": 1 3 3 2 1 2 3 1 3 2 ...
     $ angina   : num  1 1 1 0 0 0 0 0 1 0 ...

``` r
colSums(is.na(dig_hw1))
```

    subjectid   death_f      tx_f       age    race_f    female   ejf_per 
            0         0         0         0         0         0         0 
          bmi      nyha    angina 
            1         6         2 

We need to impute six values of `nyha` (a factor), 2 of `angina` (which is a numeric indicator variable) and 1 `bmi` (which is quantitative). I'll make some arbitrary decisions about how I'll do this, as implemented below...

``` r
set.seed(5002019)

dig_imp <- dig_hw1 %>%
    impute_pmm(angina ~ ejf_per) %>%
    impute_cart(nyha ~ ejf_per) %>%
    impute_rlm(bmi ~ age + race_f + female) 

colSums(is.na(dig_imp))
```

    subjectid   death_f      tx_f       age    race_f    female   ejf_per 
            0         0         0         0         0         0         0 
          bmi      nyha    angina 
            0         0         0 

``` r
set.seed(201901312)

dig_imp_train <- sample_n(dig_imp, size = 5000)
dig_imp_test <- anti_join(dig_imp, dig_imp_train)
```

    Joining, by = c("subjectid", "death_f", "tx_f", "age", "race_f", "female", "ejf_per", "bmi", "nyha", "angina")

and now we can follow the earlier commands to fit the logistic regression model in the training set, and then assess its results in the test set.

### Fitting a Logistic Regression Model to the training sample

``` r
model2 <- glm(death_f ~ tx_f + age + race_f + female + 
                  ejf_per + bmi + nyha + angina, 
              family = binomial(link = "logit"),
              data = dig_imp_train)

summary(model2)
```


    Call:
    glm(formula = death_f ~ tx_f + age + race_f + female + ejf_per + 
        bmi + nyha + angina, family = binomial(link = "logit"), data = dig_imp_train)

    Deviance Residuals: 
        Min       1Q   Median       3Q      Max  
    -1.7077  -0.9199  -0.7451   1.2676   1.9704  

    Coefficients:
                      Estimate Std. Error z value Pr(>|z|)    
    (Intercept)      0.2719634  0.2798570   0.972  0.33115    
    tx_fTreatment   -0.0407611  0.0611523  -0.667  0.50506    
    age             -0.0035712  0.0027938  -1.278  0.20116    
    race_fNon-White -0.0369065  0.0881101  -0.419  0.67531    
    female          -0.2128858  0.0760473  -2.799  0.00512 ** 
    ejf_per         -0.0363669  0.0035667 -10.196  < 2e-16 ***
    bmi             -0.0005806  0.0058286  -0.100  0.92065    
    nyha2            0.2904711  0.1012049   2.870  0.00410 ** 
    nyha3            0.8468042  0.1068352   7.926 2.26e-15 ***
    nyha4            1.4885739  0.2225029   6.690 2.23e-11 ***
    angina          -0.1025465  0.0693956  -1.478  0.13949    
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    (Dispersion parameter for binomial family taken to be 1)

        Null deviance: 6464.5  on 4999  degrees of freedom
    Residual deviance: 6182.4  on 4989  degrees of freedom
    AIC: 6204.4

    Number of Fisher Scoring iterations: 4

``` r
glance(model2)
```

    # A tibble: 1 x 7
      null.deviance df.null logLik   AIC   BIC deviance df.residual
              <dbl>   <int>  <dbl> <dbl> <dbl>    <dbl>       <int>
    1         6465.    4999 -3091. 6204. 6276.    6182.        4989

### Applying the model to a test sample, and producing a graph

``` r
dig_imp_test$.fit2 <- predict(model2, newdata = dig_imp_test, type = "response")

ggplot(dig_imp_test, aes(x = death_f, y = .fit2, fill = death_f)) +
  geom_boxplot() + 
  guides(fill = FALSE) +
  labs(y = "Estimated `model2` Probability of Death", 
       x = "Observed Vital Status",
      title = "Boxplot of `model2` predictions for DIG study",
      subtitle = "NAs imputed")
```

![](homework1_sketch_files/figure-markdown_github/unnamed-chunk-16-1.png)
