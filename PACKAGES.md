# R Packages for 500 - Spring 2019

Copy and paste the following two lines of code into the Console window of R Studio to install the packages you'll need for this course.

<!-- -->

    pkgs <- c(  "afex", "aplpack", "arm", "babynames", "boot", "car", "CBPS", "cobalt", "cowplot",
                "devtools", "ebal", "Epi", "ez", "faraway", "fivethirtyeight", "foreign", "gapminder", 
                "gee", "geepack", "GGally", "ggrepel", "ggridges", "ggthemes", "glue", "gridExtra", "here", 
                "Hmisc", "infer", "knitr", "lars", "lattice", "leaps", "lme4", "lmerTest", "magrittr", 
                "markdown", "MASS", "Matching", "MatchIt", "mice", "mosaic", "multcomp", "NHANES", "optmatch", 
                "pander", "pROC", "pscl", "psych", "pwr", "qcc", "QuantPsyc", "rbounds", "rmarkdown", 
                "rms", "ROCR", "rstanarm", "sandwich", "simputation", "skimr", "spelling", "styler", 
                "survey", "survival", "survminer", "tableone", "tidyverse", "twang", "usethis", "vcd", "viridis")

    install.packages(pkgs)

1.  Now, go to the **Packages** tab on the right side of your screen, and click on **Update**. Select and install all available updates.

2.  Finally, choose **File ... Quit R** from the top menu, and accept R Studio's request to save your workspace. This will eliminate the need to re-do these steps every time you work in R.

Note: If you want to install a single package, you can do so by finding the word **Packages** on the right side of your screen. Click on the **Packages** menu to start installing the packages you'll need. Then click **Install**, which will bring up a dialog box, where you can type in the names of the packages that you need. these should be separated by a space or comma. - Be sure to leave the Install dependencies box checked.

## A Note on the `rmdformats` package

Until further notice, you should install the development version of `rmdformats` from Github by typing `devtools::install_github("juba/rmdformats")` into the R Console after completing the steps above.
